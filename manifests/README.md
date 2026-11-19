# Public install/update manifest V1

Public immutable-path contract for distributed apps and the generic Installer.

- Stable discovery: `manifests/<applicationId>/<channel>.json`, for example `manifests/remvibe_flutter_ui/internal.json` on the public repository's `main` branch.
- `schemaVersion: 1` and the JSON meaning of existing fields MUST remain supported. Additive optional fields may be added. Unknown optional fields must be ignored by V1 readers; unknown schema major versions are unsupported, never silently coerced.
- `latest` is the current version per platform/architecture; `versions` retains already published entries. Do not remove a previously offered V1 URL or rewrite a published version to point at different bytes.
- Each version supplies `installers[]` and `updates[]` with exact artifact URLs, file sizes, SHA-256, and detached Release V1 sidecars. The same verified NTA may serve both. The mutable public index supports discovery only; it NEVER authorizes installation or update on its own. Consumers must verify pinned publisher Ed25519 Release V1 metadata/signature, target and NTA contents before mutation.
- Publish verified signed NTA, Release V1 metadata and signature FIRST; update `latest` in the public manifest LAST. If publication fails, keep the previous manifest unchanged.
- For breaking changes, ship a separate V2 document/URL, retaining V1 and a supported V1 publication projection for already deployed clients. Do not move the V1 path or repurpose its existing fields.
- `presentation.logoUrl` points to an actual public application icon; branding is presentation data and is never trusted as executable update authority.

This first manifest records only signed existing releases of the Windows Flutter UI Example on `internal`. This branch is not public-production acceptance until both actual Installer and Updater consumers exercise it and operator accepts the full install/update flow.
