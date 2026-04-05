# project-registry

Static project registry hosted as JSON files. Consumed by [@ddproxy/registry-client](https://github.com/ddproxy/registry-client).

## Registry structure

```
index.json                              # list of all project slugs
projects/
  {slug}.json                           # ProjectMetadata
  {slug}/
    versions/
      index.json                        # VersionMetadata[] for all versions
      {version}.json                    # VersionMetadata for a single version
```

## Workflows

Records are managed via workflow dispatch using [registry-actions](https://github.com/ddproxy/registry-actions). All operations use upsert semantics — create on first run, patch on subsequent runs.

### Upsert Project

**Actions → Upsert Project** — creates or updates a project record.

| Field | Notes |
|-------|-------|
| `project_name` | Required. Slug — lowercase, hyphens only. |
| `display_name` | Optional. Auto-generated from slug if blank on create. |
| `description` | Optional. |
| `repo_github` | Optional. |
| `repo_gitea` | Optional. |
| `tags` | Optional. Comma-separated. Replaces existing tags when provided. |
| `license` | Optional. Defaults to `MIT` on create. |

### Upsert Version

**Actions → Upsert Version** — creates or updates a version record.

| Field | Notes |
|-------|-------|
| `project_name` | Required. |
| `version` | Required. E.g. `v1.2.0`. |
| `changelog` | Optional on update. One entry per line. |
| `asset_source` | Required on create. Source tarball URL. |
| `asset_binary` | Optional. |
| `repo_tag_github` | Optional. |
| `repo_tag_gitea` | Optional. |
| `license` | Optional. Defaults to `MIT` on create. |

## Automated registration

Projects that include the [project-template](https://github.com/ddproxy/project-template) workflows register new versions automatically on every `v*` tag push — no manual dispatch needed.

## Required secrets

| Secret | Purpose |
|--------|---------|
| `REGISTRY_TOKEN` | Token with write access to this repository (used by calling repos) |
