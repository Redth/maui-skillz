# .NET MAUI Workload Release Notes - March 10, 2026

> **Date:** March 10, 2026  
> **Source:** NuGet.org workload manifests + Azure DevOps dotnet-workloads feed (live data)

This document provides version information for the .NET MAUI workload updates published for this release.

⬅️ [Back to Release Notes Index](maui-release-notes.md)

---

# .NET 11 (Preview 2)

**Workload Set:** [Microsoft.NET.Workloads.11.0.100-preview.2](https://dev.azure.com/dnceng/public/_artifacts/feed/dotnet-workloads/NuGet/Microsoft.NET.Workloads.11.0.100-preview.2/overview/11.100.0-preview.2.26160.1) version `11.100.0-preview.2.26160.1` (CLI: `11.0.100-preview.2.26160.1`)

The Preview 2 workload set is available from the public Azure DevOps `dotnet-workloads` feed, while the individual Preview 2 manifest packages are published on NuGet.org. Official .NET 11 release metadata still reported Preview 1 at the time of writing.

## MAUI NuGet Packages

The following NuGet packages are the core .NET MAUI libraries. The **Implicit Version** is bundled with the workload, while **Latest Version** may be newer due to out-of-band releases.

| Package | Implicit Version | Latest Version | Release Notes |
|---------|------------------|----------------|---------------|
| Microsoft.Maui.Controls | [11.0.0-preview.2.26152.10](https://www.nuget.org/packages/Microsoft.Maui.Controls/11.0.0-preview.2.26152.10) | [11.0.0-preview.2.26152.10](https://www.nuget.org/packages/Microsoft.Maui.Controls/11.0.0-preview.2.26152.10) | |
| Microsoft.Maui.Controls.Compatibility | [11.0.0-preview.2.26152.10](https://www.nuget.org/packages/Microsoft.Maui.Controls.Compatibility/11.0.0-preview.2.26152.10) | [11.0.0-preview.2.26152.10](https://www.nuget.org/packages/Microsoft.Maui.Controls.Compatibility/11.0.0-preview.2.26152.10) | |
| Microsoft.Maui.Essentials | [11.0.0-preview.2.26152.10](https://www.nuget.org/packages/Microsoft.Maui.Essentials/11.0.0-preview.2.26152.10) | [11.0.0-preview.2.26152.10](https://www.nuget.org/packages/Microsoft.Maui.Essentials/11.0.0-preview.2.26152.10) | |
| Microsoft.Maui.Graphics | [11.0.0-preview.2.26152.10](https://www.nuget.org/packages/Microsoft.Maui.Graphics/11.0.0-preview.2.26152.10) | [11.0.0-preview.2.26152.10](https://www.nuget.org/packages/Microsoft.Maui.Graphics/11.0.0-preview.2.26152.10) | |
| Microsoft.Maui.Maps | [11.0.0-preview.2.26152.10](https://www.nuget.org/packages/Microsoft.Maui.Maps/11.0.0-preview.2.26152.10) | [11.0.0-preview.2.26152.10](https://www.nuget.org/packages/Microsoft.Maui.Maps/11.0.0-preview.2.26152.10) | |

## Workload Versions

| Workload | Full ID | Version | SDK Band | Links |
|----------|---------|---------|----------|-------|
| **MAUI** | Microsoft.NET.Sdk.Maui | 11.0.0-preview.2.26152.10 | 11.0.100-preview.2 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.Maui.Manifest-11.0.100-preview.2/11.0.0-preview.2.26152.10) |
| **iOS** | Microsoft.NET.Sdk.iOS | 26.2.11425-net11-p2 | 11.0.100-preview.2 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.iOS.Manifest-11.0.100-preview.2/26.2.11425-net11-p2) |
| **Mac Catalyst** | Microsoft.NET.Sdk.MacCatalyst | 26.2.11425-net11-p2 | 11.0.100-preview.2 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.MacCatalyst.Manifest-11.0.100-preview.2/26.2.11425-net11-p2) |
| **Android** | Microsoft.NET.Sdk.Android | 36.1.99-preview.2.154 | 11.0.100-preview.2 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.Android.Manifest-11.0.100-preview.2/36.1.99-preview.2.154) · [Release](https://github.com/dotnet/android/releases/tag/36.1.99-preview.2.154) |
| **tvOS** | Microsoft.NET.Sdk.tvOS | 26.2.11425-net11-p2 | 11.0.100-preview.2 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.tvOS.Manifest-11.0.100-preview.2/26.2.11425-net11-p2) |
| **macOS** | Microsoft.NET.Sdk.macOS | 26.2.11425-net11-p2 | 11.0.100-preview.2 | [NuGet](https://www.nuget.org/packages/Microsoft.NET.Sdk.macOS.Manifest-11.0.100-preview.2/26.2.11425-net11-p2) |

> Note: Public GitHub release tags were available for Android Preview 2, but not for the corresponding MAUI or macios Preview 2 packages at the time of writing.

## Installation

Because the Preview 2 workload set is currently available from the public Azure DevOps `dotnet-workloads` feed while the manifest packages are published on NuGet.org, include both sources when installing or updating workloads.

```bash
# Update existing workloads to this version
dotnet workload update \
  --source https://pkgs.dev.azure.com/dnceng/public/_packaging/dotnet-workloads/nuget/v3/index.json \
  --source https://api.nuget.org/v3/index.json \
  --version 11.0.100-preview.2.26160.1

# Or install specific workloads
dotnet workload install maui ios maccatalyst android \
  --source https://pkgs.dev.azure.com/dnceng/public/_packaging/dotnet-workloads/nuget/v3/index.json \
  --source https://api.nuget.org/v3/index.json \
  --version 11.0.100-preview.2.26160.1
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
| **JDK** | ≥ 21.0 and < 22.0 | 21.0.8 |

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
| **Windows App SDK** | ≥ 1.8.251106002 | 1.8.251106002 |
| **Windows SDK Build Tools** | ≥ 10.0.26100.4654 | 10.0.26100.4654 |
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

- [Microsoft.NET.Workloads.11.0.100-preview.2](https://dev.azure.com/dnceng/public/_artifacts/feed/dotnet-workloads/NuGet/Microsoft.NET.Workloads.11.0.100-preview.2/overview/11.100.0-preview.2.26160.1) version `11.100.0-preview.2.26160.1` (CLI: `11.0.100-preview.2.26160.1`)
- [Microsoft.NET.Sdk.Maui.Manifest-11.0.100-preview.2](https://www.nuget.org/packages/Microsoft.NET.Sdk.Maui.Manifest-11.0.100-preview.2/11.0.0-preview.2.26152.10) version `11.0.0-preview.2.26152.10`
- [Microsoft.NET.Sdk.iOS.Manifest-11.0.100-preview.2](https://www.nuget.org/packages/Microsoft.NET.Sdk.iOS.Manifest-11.0.100-preview.2/26.2.11425-net11-p2) version `26.2.11425-net11-p2`
- [Microsoft.NET.Sdk.MacCatalyst.Manifest-11.0.100-preview.2](https://www.nuget.org/packages/Microsoft.NET.Sdk.MacCatalyst.Manifest-11.0.100-preview.2/26.2.11425-net11-p2) version `26.2.11425-net11-p2`
- [Microsoft.NET.Sdk.tvOS.Manifest-11.0.100-preview.2](https://www.nuget.org/packages/Microsoft.NET.Sdk.tvOS.Manifest-11.0.100-preview.2/26.2.11425-net11-p2) version `26.2.11425-net11-p2`
- [Microsoft.NET.Sdk.macOS.Manifest-11.0.100-preview.2](https://www.nuget.org/packages/Microsoft.NET.Sdk.macOS.Manifest-11.0.100-preview.2/26.2.11425-net11-p2) version `26.2.11425-net11-p2`
- [Microsoft.NET.Sdk.Android.Manifest-11.0.100-preview.2](https://www.nuget.org/packages/Microsoft.NET.Sdk.Android.Manifest-11.0.100-preview.2/36.1.99-preview.2.154) version `36.1.99-preview.2.154`
- [.NET 11 release metadata](https://dotnetcli.blob.core.windows.net/dotnet/release-metadata/releases-index.json) still reported `11.0.100-preview.1.26104.118` as the latest SDK at the time of writing
