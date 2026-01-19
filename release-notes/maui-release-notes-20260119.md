# .NET MAUI Workload Release Notes - January 19, 2026

> **Date:** January 19, 2026  
> **Source:** NuGet.org workload manifests (live data)

This document provides version information for .NET MAUI and related platform workloads across the two most recent major .NET versions.

⬅️ [Back to Release Notes Index](maui-release-notes.md)

---

# .NET 10

**Workload Set:** [Microsoft.NET.Workloads.10.0.100](https://www.nuget.org/packages/Microsoft.NET.Workloads.10.0.100/10.102.0) version `10.102.0`

## MAUI NuGet Packages

The following NuGet packages are the core .NET MAUI libraries. The **Implicit Version** is bundled with the workload, while **Latest Version** may be newer due to out-of-band releases.

| Package | Implicit Version | Latest Version | Release Notes |
|---------|------------------|----------------|---------------|
| Microsoft.Maui.Controls | [10.0.1](https://www.nuget.org/packages/Microsoft.Maui.Controls/10.0.1) | [10.0.30](https://www.nuget.org/packages/Microsoft.Maui.Controls/10.0.30) | [GitHub](https://github.com/dotnet/maui/releases/tag/10.0.30) |
| Microsoft.Maui.Controls.Compatibility | [10.0.1](https://www.nuget.org/packages/Microsoft.Maui.Controls.Compatibility/10.0.1) | [10.0.30](https://www.nuget.org/packages/Microsoft.Maui.Controls.Compatibility/10.0.30) | |
| Microsoft.Maui.Essentials | [10.0.1](https://www.nuget.org/packages/Microsoft.Maui.Essentials/10.0.1) | [10.0.30](https://www.nuget.org/packages/Microsoft.Maui.Essentials/10.0.30) | |
| Microsoft.Maui.Graphics | [10.0.1](https://www.nuget.org/packages/Microsoft.Maui.Graphics/10.0.1) | [10.0.30](https://www.nuget.org/packages/Microsoft.Maui.Graphics/10.0.30) | |
| Microsoft.Maui.Maps | [10.0.1](https://www.nuget.org/packages/Microsoft.Maui.Maps/10.0.1) | [10.0.30](https://www.nuget.org/packages/Microsoft.Maui.Maps/10.0.30) | |

## Workload Versions

| Workload | Full ID | Version | SDK Band | Links |
|----------|---------|---------|----------|-------|
| **MAUI** | Microsoft.NET.Sdk.Maui | 10.0.1 | 10.0.100 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.Maui.Manifest-10.0.100/10.0.1) · [Release](https://github.com/dotnet/maui/releases/tag/10.0.1) |
| **iOS** | Microsoft.NET.Sdk.iOS | 26.2.10191 | 10.0.100 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.iOS.Manifest-10.0.100/26.2.10191) · [Release](https://github.com/dotnet/macios/releases/tag/dotnet-10.0.1xx-xcode26.2-10191) |
| **Mac Catalyst** | Microsoft.NET.Sdk.MacCatalyst | 26.2.10191 | 10.0.100 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.MacCatalyst.Manifest-10.0.100/26.2.10191) · [Release](https://github.com/dotnet/macios/releases/tag/dotnet-10.0.1xx-xcode26.2-10191) |
| **Android** | Microsoft.NET.Sdk.Android | 36.1.12 | 10.0.100 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.Android.Manifest-10.0.100/36.1.12) · [Release](https://github.com/dotnet/android/releases/tag/36.1.12) |
| **tvOS** | Microsoft.NET.Sdk.tvOS | 26.2.10191 | 10.0.100 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.tvOS.Manifest-10.0.100/26.2.10191) · [Release](https://github.com/dotnet/macios/releases/tag/dotnet-10.0.1xx-xcode26.2-10191) |
| **macOS** | Microsoft.NET.Sdk.macOS | 26.2.10191 | 10.0.100 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.macOS.Manifest-10.0.100/26.2.10191) · [Release](https://github.com/dotnet/macios/releases/tag/dotnet-10.0.1xx-xcode26.2-10191) |

## Installation

```bash
# Update existing workloads to this version
dotnet workload update --version 10.0.102

# Or install specific workloads
dotnet workload install maui ios maccatalyst android --version 10.0.102
```

## Apple Platform Dependencies (iOS, Mac Catalyst, tvOS, macOS)

Apple platform workloads require Xcode to be installed.

| Workload | Xcode Requirement | Recommended Xcode | Apple SDK |
|----------|-------------------|-------------------|-----------|
| iOS | ≥ 26.2 | 26.2 | 26.2 |
| Mac Catalyst | ≥ 26.2 | 26.2 | 26.2 |
| tvOS | ≥ 26.2 | 26.2 | 26.2 |
| macOS | ≥ 26.2 | 26.2 | 26.2 |

## Android Dependencies

| Dependency | Requirement | Recommended |
|------------|-------------|-------------|
| **JDK** | ≥ 17.0 and < 22.0 | 17.0.14 |

### Required Android SDK Packages

| Package | Description |
|---------|-------------|
| `build-tools;36.0.0` | Android SDK Build-Tools 36 |
| `cmdline-tools;19.0` | Android SDK Command-line Tools |
| `platforms;android-36` | Android SDK Platform 36 |
| `platform-tools` | Android SDK Platform-Tools (recommended: 36.0.0) |

### Optional Android SDK Packages

| Package | Description |
|---------|-------------|
| `emulator` | Android Emulator (recommended: 36.2.12) |
| `ndk-bundle` | NDK (recommended: 27.2.12479018) |
| `platforms;android-36.1` | Android SDK Platform 36.1 (Preview) |
| System Images | Google APIs ARM 64 v8a / x86_64 for android-36.1 |

## MAUI Windows Dependencies

| Dependency | Minimum Version | Recommended |
|------------|-----------------|-------------|
| **Windows App SDK** | ≥ 1.7.250909003 | 1.7.250909003 |
| **Windows SDK Build Tools** | ≥ 10.0.22621.756 | 10.0.22621.756 |
| **Win2D** | ≥ 1.3.2 | 1.3.2 |
| **WebView2** | ≥ 1.0.3179.45 | 1.0.3179.45 |

## Appium Testing Dependencies (Optional)

| Component | Minimum Version | Recommended |
|-----------|-----------------|-------------|
| **Appium** | ≥ 2.17.1 | 2.17.1 |
| **Windows Driver** | ≥ 3.1.1 | 3.1.1 |
| **XCUITest Driver** | ≥ 7.32.0 | 7.32.0 |
| **Mac2 Driver** | ≥ 1.20.3 | 1.20.3 |
| **UIAutomator2 Driver** | ≥ 4.2.1 | 4.2.1 |

## Data Sources

- [Microsoft.NET.Workloads.10.0.100](https://www.nuget.org/packages/Microsoft.NET.Workloads.10.0.100/10.102.0) version `10.102.0`
- [Microsoft.NET.Sdk.Maui.Manifest-10.0.100](https://www.nuget.org/packages/Microsoft.NET.Sdk.Maui.Manifest-10.0.100/10.0.1) version `10.0.1`
- [Microsoft.NET.Sdk.iOS.Manifest-10.0.100](https://www.nuget.org/packages/Microsoft.NET.Sdk.iOS.Manifest-10.0.100/26.2.10191) version `26.2.10191`
- [Microsoft.NET.Sdk.Android.Manifest-10.0.100](https://www.nuget.org/packages/Microsoft.NET.Sdk.Android.Manifest-10.0.100/36.1.12) version `36.1.12`

---

# .NET 9

**Workload Set:** [Microsoft.NET.Workloads.9.0.300](https://www.nuget.org/packages/Microsoft.NET.Workloads.9.0.300/9.309.0) version `9.309.0`

## MAUI NuGet Packages

The following NuGet packages are the core .NET MAUI libraries. The **Implicit Version** is bundled with the workload, while **Latest Version** may be newer due to out-of-band releases.

| Package | Implicit Version | Latest Version | Release Notes |
|---------|------------------|----------------|---------------|
| Microsoft.Maui.Controls | [9.0.120](https://www.nuget.org/packages/Microsoft.Maui.Controls/9.0.120) | [9.0.120](https://www.nuget.org/packages/Microsoft.Maui.Controls/9.0.120) | [GitHub](https://github.com/dotnet/maui/releases/tag/9.0.120) |
| Microsoft.Maui.Controls.Compatibility | [9.0.120](https://www.nuget.org/packages/Microsoft.Maui.Controls.Compatibility/9.0.120) | [9.0.120](https://www.nuget.org/packages/Microsoft.Maui.Controls.Compatibility/9.0.120) | |
| Microsoft.Maui.Essentials | [9.0.120](https://www.nuget.org/packages/Microsoft.Maui.Essentials/9.0.120) | [9.0.120](https://www.nuget.org/packages/Microsoft.Maui.Essentials/9.0.120) | |
| Microsoft.Maui.Graphics | [9.0.120](https://www.nuget.org/packages/Microsoft.Maui.Graphics/9.0.120) | [9.0.120](https://www.nuget.org/packages/Microsoft.Maui.Graphics/9.0.120) | |
| Microsoft.Maui.Maps | [9.0.120](https://www.nuget.org/packages/Microsoft.Maui.Maps/9.0.120) | [9.0.120](https://www.nuget.org/packages/Microsoft.Maui.Maps/9.0.120) | |

## Workload Versions

| Workload | Full ID | Version | SDK Band | Links |
|----------|---------|---------|----------|-------|
| **MAUI** | Microsoft.NET.Sdk.Maui | 9.0.120 | 9.0.100 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.Maui.Manifest-9.0.100/9.0.120) · [Release](https://github.com/dotnet/maui/releases/tag/9.0.120) |
| **iOS** | Microsoft.NET.Sdk.iOS | 26.0.9783 | 9.0.100 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.iOS.Manifest-9.0.100/26.0.9783) · [Release](https://github.com/dotnet/macios/releases/tag/dotnet-9.0.1xx-xcode26.0-9783) |
| **Mac Catalyst** | Microsoft.NET.Sdk.MacCatalyst | 26.0.9783 | 9.0.100 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.MacCatalyst.Manifest-9.0.100/26.0.9783) · [Release](https://github.com/dotnet/macios/releases/tag/dotnet-9.0.1xx-xcode26.0-9783) |
| **Android** | Microsoft.NET.Sdk.Android | 35.0.105 | 9.0.100 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.Android.Manifest-9.0.100/35.0.105) · [Release](https://github.com/dotnet/android/releases/tag/35.0.105) |
| **tvOS** | Microsoft.NET.Sdk.tvOS | 26.0.9783 | 9.0.100 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.tvOS.Manifest-9.0.100/26.0.9783) · [Release](https://github.com/dotnet/macios/releases/tag/dotnet-9.0.1xx-xcode26.0-9783) |
| **macOS** | Microsoft.NET.Sdk.macOS | 26.0.9783 | 9.0.100 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.macOS.Manifest-9.0.100/26.0.9783) · [Release](https://github.com/dotnet/macios/releases/tag/dotnet-9.0.1xx-xcode26.0-9783) |

## Installation

```bash
# Update existing workloads to this version
dotnet workload update --version 9.0.309

# Or install specific workloads
dotnet workload install maui ios maccatalyst android --version 9.0.309
```

## Apple Platform Dependencies (iOS, Mac Catalyst, tvOS, macOS)

Apple platform workloads require Xcode to be installed.

| Workload | Xcode Requirement | Recommended Xcode | Apple SDK |
|----------|-------------------|-------------------|-----------|
| iOS | ≥ 26.0 | 26.0 | 26.0 |
| Mac Catalyst | ≥ 26.0 | 26.0 | 26.0 |
| tvOS | ≥ 26.0 | 26.0 | 26.0 |
| macOS | ≥ 26.0 | 26.0 | 26.0 |

## Android Dependencies

| Dependency | Requirement | Recommended |
|------------|-------------|-------------|
| **JDK** | ≥ 17.0 and < 22.0 | 17.0.14 |

### Required Android SDK Packages

| Package | Description |
|---------|-------------|
| `build-tools;35.0.0` | Android SDK Build-Tools 35 |
| `cmdline-tools;12.0` | Android SDK Command-line Tools |
| `platforms;android-35` | Android SDK Platform 35 |
| `platform-tools` | Android SDK Platform-Tools (recommended: 34.0.5) |

### Optional Android SDK Packages

| Package | Description |
|---------|-------------|
| `emulator` | Android Emulator (recommended: 35.1.20) |
| `ndk;26.1.10909125` | NDK (Side by side) 26.1 |
| `platforms;android-36` | Android SDK Platform 36 (Preview) |
| System Images | Google APIs ARM 64 v8a / x86_64 for android-35 |

## MAUI Windows Dependencies

| Dependency | Minimum Version | Recommended |
|------------|-----------------|-------------|
| **Windows App SDK** | ≥ 1.7.250909003 | 1.7.250909003 |
| **Windows SDK Build Tools** | ≥ 10.0.22621.756 | 10.0.22621.756 |
| **Win2D** | ≥ 1.3.2 | 1.3.2 |
| **WebView2** | ≥ 1.0.3179.45 | 1.0.3179.45 |

## Appium Testing Dependencies (Optional)

| Component | Minimum Version | Recommended |
|-----------|-----------------|-------------|
| **Appium** | ≥ 2.17.1 | 2.17.1 |
| **Windows Driver** | ≥ 3.1.1 | 3.1.1 |
| **XCUITest Driver** | ≥ 7.32.0 | 7.32.0 |
| **Mac2 Driver** | ≥ 1.20.3 | 1.20.3 |
| **UIAutomator2 Driver** | ≥ 4.2.1 | 4.2.1 |

## Data Sources

- [Microsoft.NET.Workloads.9.0.300](https://www.nuget.org/packages/Microsoft.NET.Workloads.9.0.300/9.309.0) version `9.309.0`
- [Microsoft.NET.Sdk.Maui.Manifest-9.0.100](https://www.nuget.org/packages/Microsoft.NET.Sdk.Maui.Manifest-9.0.100/9.0.120) version `9.0.120`
- [Microsoft.NET.Sdk.iOS.Manifest-9.0.100](https://www.nuget.org/packages/Microsoft.NET.Sdk.iOS.Manifest-9.0.100/26.0.9783) version `26.0.9783`
- [Microsoft.NET.Sdk.Android.Manifest-9.0.100](https://www.nuget.org/packages/Microsoft.NET.Sdk.Android.Manifest-9.0.100/35.0.105) version `35.0.105`

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
