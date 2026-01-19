---
name: maui-workload-discovery
description: Discover .NET SDK versions, workload sets, workload manifest versions, and workload dependencies (Xcode/JDK/Android SDK) for MAUI release docs and environment validation. Use when asked about .NET MAUI requirements, dotnet SDK requirements and versions, dotnet workload sets / version sets, dotnet workload versions and manifest versions, dotnet workload dependencies such as Xcode versions, Android SDK packages, JDK versions, or other native tools and sdks.
---

# When to use this skill
Activate this skill when the user asks:
- What Xcode version is required for .NET X?
- What Android SDK packages are needed for .NET MAUI?
- What JDK version is required?
- What is the latest workload set for .NET X?
- What workload versions ship with .NET X?
- How do I find the WorkloadDependencies.json for a workload?
- What is the latest .NET SDK for version X?
- What SDK versions are available for .NET X?
- What is the latest MAUI NuGet package version?
- What is the latest Microsoft.Maui.Controls version for .NET X?

# Inputs
| Parameter | Required | Example | Notes |
|-----------|----------|---------|-------|
| dotnetVersion | yes | 9.0, 10.0 | Major.minor format |
| prerelease | no | true/false | Default false; set true for preview SDKs |
| workload | no | ios, android, maui | Alias or full id |

# Workload alias mapping
| Alias | Full ID |
|-------|---------|
| ios | microsoft.net.sdk.ios |
| android | microsoft.net.sdk.android |
| maccatalyst | microsoft.net.sdk.maccatalyst |
| macos | microsoft.net.sdk.macos |
| tvos | microsoft.net.sdk.tvos |
| maui | microsoft.net.sdk.maui |

# Step-by-step process

## Step 0: Discover available .NET SDK versions (optional but recommended)
Use the official .NET releases JSON to find available SDK versions for a major version.

### Releases index
```
GET https://dotnetcli.blob.core.windows.net/dotnet/release-metadata/releases-index.json
```

Response contains an array of channels:
```json
{
  "releases-index": [
    {
      "channel-version": "10.0",
      "latest-release": "10.0.2",
      "latest-sdk": "10.0.102",
      "support-phase": "active",
      "release-type": "lts",
      "releases.json": "https://builds.dotnet.microsoft.com/dotnet/release-metadata/10.0/releases.json"
    }
  ]
}
```

Key fields:
| Field | Description |
|-------|-------------|
| `channel-version` | Major.minor version (e.g., "10.0") |
| `latest-sdk` | Latest stable SDK version (e.g., "10.0.102") |
| `latest-release` | Latest runtime release version |
| `support-phase` | "active", "maintenance", "eol" |
| `release-type` | "lts" or "sts" |
| `releases.json` | URL to detailed release info |

### Per-channel releases detail
Fetch the `releases.json` URL for full SDK history:
```
GET https://builds.dotnet.microsoft.com/dotnet/release-metadata/{major}.0/releases.json
```

Response contains a `releases` array with each release having:
```json
{
  "release-version": "10.0.2",
  "sdk": {
    "version": "10.0.102",
    "runtime-version": "10.0.2"
  },
  "sdks": [
    { "version": "10.0.102" },
    { "version": "10.0.101" }
  ]
}
```

### SDK band derivation
From an SDK version like `10.0.102`:
- SDK band = `{major}.0.{feature_band}` where feature_band is the hundreds digit
- Example: `10.0.102` → band `10.0.100`
- Example: `10.0.205` → band `10.0.200`

### Quick lookup algorithm
1. Fetch releases-index.json
2. Find entry where `channel-version` matches requested major version
3. Use `latest-sdk` for the current stable SDK
4. Derive SDK band from SDK version
5. Use band to find workload set packages

## Step 1: Find workload set packages
Search NuGet for workload set packages:
```
GET https://azuresearch-usnc.nuget.org/query?q=Microsoft.NET.Workloads.{major}.0&prerelease=false&semVerLevel=2.0.0
```
Example for .NET 10:
```
https://azuresearch-usnc.nuget.org/query?q=Microsoft.NET.Workloads.10.0&prerelease=false&semVerLevel=2.0.0
```

Filter results:
- Include only packages matching `Microsoft.NET.Workloads.{major}.{band}` (e.g., `Microsoft.NET.Workloads.10.0.100`)
- Exclude MSI packages (`.Msi.x64`, `.Msi.arm64`)
- Pick highest version

## Step 2: Convert NuGet version to CLI version
NuGet version format: `{major}.{patch}.{revision}` (e.g., `10.102.0`)
CLI version format: `{major}.0.{patch}` (e.g., `10.0.102`)

Conversion:
```
parts = nugetVersion.split('.')
cliVersion = parts[0] + ".0." + parts[1]
```

## Step 3: Download and extract workload set manifest
Download URL pattern (all lowercase):
```
https://api.nuget.org/v3-flatcontainer/{packageid}/{version}/{packageid}.{version}.nupkg
```
Example:
```
https://api.nuget.org/v3-flatcontainer/microsoft.net.workloads.10.0.100/10.102.0/microsoft.net.workloads.10.0.100.10.102.0.nupkg
```

The .nupkg is a ZIP file. Extract and read:
```
data/microsoft.net.workloads.workloadset.json
```

Contents example:
```json
{
  "microsoft.net.sdk.android": "35.0.50/9.0.100",
  "microsoft.net.sdk.ios": "26.2.10191/10.0.100",
  "microsoft.net.sdk.maui": "10.0.10/10.0.100"
}
```
Format: `"{workload_id}": "{manifestVersion}/{sdkBand}"`

## Step 4: Download workload manifest package
Build manifest package id:
```
{WorkloadId}.Manifest-{sdkBand}
```
Examples:
- `Microsoft.NET.Sdk.iOS.Manifest-10.0.100`
- `Microsoft.NET.Sdk.Android.Manifest-9.0.100`

Download URL:
```
https://api.nuget.org/v3-flatcontainer/microsoft.net.sdk.ios.manifest-10.0.100/26.2.10191/microsoft.net.sdk.ios.manifest-10.0.100.26.2.10191.nupkg
```

## Step 5: Extract WorkloadDependencies.json
From the manifest .nupkg, extract:
```
data/WorkloadDependencies.json
```

### Android dependencies structure
```json
{
  "microsoft.net.sdk.android": {
    "jdk": {
      "version": "[17.0,22.0)",
      "recommendedVersion": "17.0.14"
    },
    "androidsdk": {
      "packages": ["build-tools;35.0.0", "platform-tools", "platforms;android-35", "cmdline-tools;13.0"],
      "apiLevel": "35",
      "buildToolsVersion": "35.0.0",
      "cmdLineToolsVersion": "13.0"
    }
  }
}
```

### Apple (iOS/macOS/tvOS) dependencies structure
```json
{
  "microsoft.net.sdk.ios": {
    "xcode": {
      "version": "[26.2,)",
      "recommendedVersion": "26.2"
    },
    "sdk": {
      "version": "26.2"
    }
  }
}
```

### Version range notation
| Notation | Meaning |
|----------|---------|
| `[17.0,22.0)` | >= 17.0 AND < 22.0 |
| `[26.2,)` | >= 26.2 (no upper bound) |

# CLI commands for manual inspection

## Fetch SDK versions
```bash
curl -s "https://dotnetcli.blob.core.windows.net/dotnet/release-metadata/releases-index.json" | jq '.["releases-index"][] | select(.["channel-version"]=="10.0")'
```

## Download and extract a NuGet package
```bash
curl -o package.nupkg "https://api.nuget.org/v3-flatcontainer/{id}/{version}/{id}.{version}.nupkg"
unzip package.nupkg -d extracted/
cat extracted/data/WorkloadDependencies.json
```

# Output format
Return structured data with:
- dotnetVersion
- latestSdk (version from releases-index)
- sdkBand (derived from SDK version)
- workloadSet (packageId, nugetVersion, cliVersion)
- workloads array with:
  - workloadId
  - manifestVersion
  - sdkBand
  - manifestPackageId
  - dependencies (parsed from WorkloadDependencies.json)
- mauiNugets (optional, when MAUI packages are relevant):
  - packageId
  - latestVersion
  - workloadVersion (for comparison)

## Example output
```json
{
  "dotnetVersion": "10.0",
  "latestSdk": "10.0.102",
  "sdkBand": "10.0.100",
  "workloadSet": {
    "packageId": "Microsoft.NET.Workloads.10.0.100",
    "nugetVersion": "10.102.0",
    "cliVersion": "10.0.102"
  },
  "workloads": [
    {
      "workloadId": "microsoft.net.sdk.ios",
      "manifestVersion": "26.2.10191",
      "sdkBand": "10.0.100",
      "manifestPackageId": "Microsoft.NET.Sdk.iOS.Manifest-10.0.100",
      "dependencies": {
        "xcode": {
          "versionRange": "[26.2,)",
          "recommendedVersion": "26.2"
        },
        "sdk": {
          "version": "26.2"
        }
      }
    }
  ],
  "mauiNugets": [
    {
      "packageId": "Microsoft.Maui.Controls",
      "latestVersion": "10.0.30",
      "workloadVersion": "10.0.10"
    }
  ]
}
```

# Error handling
- If NuGet search returns no results, retry with `prerelease=true`
- If WorkloadDependencies.json is missing, report explicitly
- If a dependency key is missing, note which keys are absent

# Finding latest MAUI NuGet packages

MAUI NuGet packages are sometimes updated out-of-band from the workloads and can contain new features and bug fixes. These packages are versioned to align with major .NET versions (e.g., 10.x packages require .NET 10, 9.x packages require .NET 9).

## Key MAUI NuGet packages
| Package | Description |
|---------|-------------|
| `Microsoft.Maui.Controls` | Core MAUI controls and UI framework |
| `Microsoft.Maui.Controls.Compatibility` | Compatibility layer for Xamarin.Forms migration |
| `Microsoft.Maui.Essentials` | Cross-platform APIs for device features |
| `Microsoft.Maui.Graphics` | Cross-platform graphics library |
| `Microsoft.Maui.Controls.Maps` | Map controls for MAUI |

## Query NuGet for latest package version
Use the NuGet Search API to find the latest version for a specific .NET major version:

```
GET https://azuresearch-usnc.nuget.org/query?q=packageid:Microsoft.Maui.Controls&prerelease=false&semVerLevel=2.0.0
```

Response structure:
```json
{
  "data": [
    {
      "id": "Microsoft.Maui.Controls",
      "version": "10.0.30",
      "versions": [
        { "version": "9.0.0", "@id": "..." },
        { "version": "9.0.100", "@id": "..." },
        { "version": "10.0.10", "@id": "..." },
        { "version": "10.0.30", "@id": "..." }
      ]
    }
  ]
}
```

## Filter by .NET major version
MAUI packages use semantic versioning aligned to .NET versions:
- .NET 10 → `10.x.x` (e.g., `10.0.30`)
- .NET 9 → `9.x.x` (e.g., `9.0.120`)
- .NET 8 → `8.x.x` (e.g., `8.0.100`)

To find the latest version for a specific .NET version:
1. Query NuGet for the package
2. Filter `versions` array where version starts with `{major}.`
3. Select the highest matching version

### Algorithm
```
latestForMajor = versions
  .filter(v => v.version.startsWith(majorVersion + "."))
  .sort(semverDescending)
  .first()
```

## CLI command for MAUI package lookup
```bash
# Get latest Microsoft.Maui.Controls for .NET 10
curl -s "https://azuresearch-usnc.nuget.org/query?q=packageid:Microsoft.Maui.Controls&prerelease=false" | \
  jq '.data[0].versions | map(select(.version | startswith("10."))) | last'
```

## Package metadata endpoint
For detailed package information including release notes:
```
GET https://api.nuget.org/v3/registration5-gz-semver2/microsoft.maui.controls/index.json
```

## Version comparison: Workload vs NuGet
| Source | Version | Notes |
|--------|---------|-------|
| Workload (`microsoft.net.sdk.maui`) | `10.0.10` | Bundled with SDK, updated via `dotnet workload update` |
| NuGet (`Microsoft.Maui.Controls`) | `10.0.30` | Can be newer, explicit PackageReference in .csproj |

When the NuGet package version is higher than the workload version, users can explicitly reference the newer package in their project file:
```xml
<PackageReference Include="Microsoft.Maui.Controls" Version="10.0.30" />
```

# Best practices
- ALWAYS fetch live data from NuGet; never use hard-coded versions
- ALWAYS include sdkBand with every manifest version
- Prefer stable versions unless user requests previews
- Show the user the exact URLs used for transparency

# Reference
See docs/workload-discovery-process.md for detailed background.
