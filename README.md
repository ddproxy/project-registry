# Project Registry

A static project registry hosted as a set of JSON files.

## Workflows

This repository includes workflows to manage the registry records.

### Add Project
Can be manually triggered to add a new project metadata file.

### Add Version
Can be manually triggered to add a new version record for an existing project.

## How it works

These workflows use the generic [registry-actions](https://github.com/ddproxy/registry-actions) to update the JSON files in this repository.
The registry files follow the structure expected by `@ddproxy/registry-client`.
