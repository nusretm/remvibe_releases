# Public install + update manifests — V1

**Public stable resource paths, independent of the private project catalog.**

```text
releases/<projectId>/
  installer/
    manifest.json                     # project identity and display only
    resources/
      logo.png
      sidebar.png                     # optional when supplied in Console
  updates/
    <channel>/
      list-<os>-<arch>.json           # versions + verified release assets
```

- Installer metadata has project ID, name, description, resources, and available channels, **not** the current/latest package/version.
- A generic Installer chooses the intended channel and platform/architecture, then gets `updates/<channel>/list-<os>-<arch>.json`. Installed applications read the same public list to discover updates without downloading NTA.
- This first example has a real `internal` channel matching its already-signed Release V1 metadata. `stable` and `beta` are supported as future channel directory names but cannot be populated by relabeling existing signed internal packages.
- The updates list contains version, optional `minVer`/`maxVer` eligibility bounds (null when unrestricted), exact artifact URL/size/SHA-256 and detached signed Release V1 references. No generic dependency schema or remote-command installer engine.
- Windows Installer ensures the required Microsoft VC++ runtime as a bounded built-in platform prerequisite; each application owns its other requirements. Catalog package inventory/required flags are project metadata, **not** permission for arbitrary dependency installation.
- The mutable index is discovery information only, never publisher authorization; consumers must verify the existing Release Signature V1/verified NTA before installing or updating.
- **Preservation policy:** Once V1 URLs are published and clients are deployed, never move/repurpose their paths or alter field meanings. Extend additively; for breaking changes preserve V1 while introducing a separate V2 path/version. Publish immutable signed releases first and change public version indexes last.
- Current files are in a draft feature branch only. No production client is yet bound to them and no live installation has been modified.
