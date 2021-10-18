Info
---------------------

This repository is used as a database source for Playnite's integrated add-on browser. Only add-ons submitted in this database will be visible in add-on browser and will be able to utilize add-on auto-update feature.

Submitting add-on
---------------------

To submit an add-on:
1) Navigate to appropriate add-on [directory](https://github.com/JosefNemec/PlayniteAddonDatabase/tree/master/addons).
2) Use **Add File** button and create new .yaml [addon manifest](#Addon-manifest) file.
3) Commit using **Propose new file** and create pull request

This process will create new pull request that will be awaiting a review. Once the pull request is reviewed and merged, your add-on will be visible in add-on browser. Please note that it may take a minute after the pull request is merged for add-on to be visible in add-on browser.

**NOTE** You can of course use standard git process to clone this repository and submit pull request from your fork if you are more familiar with git workflow.

### Installation URI

If you want to provide users with an easy way to directly install your add-on, you can generate special URI that will start add-on installation directly:

`playnite://playnite/installaddon/<AddonId>`

Addon manifest
---------------------

Must be properly formatted [YAML](https://en.wikipedia.org/wiki/YAML) document.

| Field | Mandatory | Description |
| :--- | :---: | :--- |
| AddonId | • | Unique ID string. Must be the same ID string used by the actual extension or theme referenced by this manifest. |
| [Type](#Add-on-types) | • | Add-on type. |
| Name | • | Add-on name. |
| Author | • | Add-on author. |
| ShortDescription | • | Short add-on description. Show on add-on list before selecting add-on details. |
| [InstallerManifestUrl](#Installer-manifest) | • | URL to installer manifest file. |
| SourceUrl | • | URL to source repository. Not mandatory for themes. |
| Description || Add-on description. |
| Tags || List of add-on tags. |
| Links || List of add-on links.  |
| [Screenshots](#Screenshot-fields) || List of add-on screenshots. |
| IconUrl || Add-on icon image URL. |
| [UserAgreement](#UserAgreement-fields) || User agreement settings if add-on requires user to agree to custom terms before add-on installation/update. |

### Add-on types

* GameLibrary
* MetadataProvider
* Generic
* ThemeDesktop
* ThemeFullscreen

### UserAgreement fields

| Field | Description |
| :--- | :--- |
| Updated | Date of last agreement update. Must be date in `YYYY-MM-DD` format. |
| AgreementUrl | URL to a text file actual agreement text. |

### Screenshot fields

| Field | Description |
| :--- | :--- |
| Thumbnail | URL to small preview image. |
| Image | URL to full image. |

### Example

```yaml
AddonId: 'SomeAddonID'
Type: GameLibrary
InstallerManifestUrl: https://addon.link/installer.yaml
ShortDescription: 'Short add-on description'
Name: 'Some Addon'
Author: 'Jane Doe'
Tags: ['tag', 'tag2', 'tag3']
SourceUrl: https://github.com/JaneDoe/SomeAddon
Links:
    Website: https://addon.link
    Website2: https://addon2.link
Screenshots:
    - Thumbnail: https://addon2.link/screenshots/thumb.jpg
      Image: https://addon2.link/screenshots/image.jpg
```

Installer manifest
---------------------

| Field | Description |
| :--- | :--- |
| AddonId | Unique ID string. Must be the same ID string used by the actual extension or theme referenced by this manifest. |
| [Packages](#Package-fields) | List of installer packages/ |

### Package fields

| Field | Description |
| :--- | :--- |
| Version | Add-on version, must be [.NET version string](https://docs.microsoft.com/en-us/dotnet/api/system.version). |
| PackageUrl | URL to an actual `.pext` or `.pthm` add-on file. |
| RequiredApiVersion | Minimal API version (SDK version or theme API version) required by this add-on version. |
| ReleaseDate | Package release date in `YYYY-MM-DD` format. |
| Changelog | List of changes. Optional. |

### Example

```yaml
AddonId: 'SomeAddonID'
Packages:
  - Version: 2.0
    RequiredApiVersion: 5.6.0
    ReleaseDate: 2021-01-25
    PackageUrl: https://addon.link/SomeAddonID_2_0.pext
    Changelog:
      - Message 1
      - Message 2
  - Version: 1.9
    RequiredApiVersion: 5.3.0
    ReleaseDate: 2021-01-20
    PackageUrl: https://addon.link/SomeAddonID_1_9.pext
    Changelog:
      - Message 3
      - Message 4
```
