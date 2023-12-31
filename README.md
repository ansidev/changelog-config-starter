# Changelog Configuration Starter

## Getting Started

This is an opinionated configuration for changelog management.

This configuration requires [conventional commits](https://www.conventionalcommits.org/).

This configuration is ideally suited for Go projects. However, you can apply it to any projects.

## Tools

These tools must be installed before using:

- [Changie](https://changie.dev/) - Automated changelog tool for preparing releases with lots of customization options.
- [git-chglog](https://github.com/git-chglog/git-chglog) - CHANGELOG generator implemented in Go.

## How it works?

- Changie is an automated changelog. However, it does not support generating changelog from git commit history.
- git-chglog will generate changelog from git commit history.
- The changelog format follow [Keep a changelog](https://keepachangelog.com/en/1.0.0/) specification.

## Manual

1. Copy all files from the directory `src/` into your root project directory.
2. Update field `info > repository_url` in `.chglog/config.yml`.
3. Update version config:

- If your project does not need the VERSION file:
  - Remove it.
  - Remove the field `replacement` and its children from `.changie.yaml`.
  - Adjust task `commit_release` in `.taskfiles/task_release.yaml`: remove/comment line `- git add {{.VERSION_FILE}}`.
- If your version file is `package.json`:
  - Remove file VERSION and use this config in `.changie.yaml`:
    ```
    replacements:
      - path: "package.json"
        find: '"version": ".*"'
        replace: '"version": "{{.VersionNoPrefix}}"'
    ```
  - Update the variable `VERSION_FILE` in `.taskfiles/task_release.yaml` to `package.json`.
- For advanced customization, please read the official documentation of each tool.

### Tasks

```
release:prepare               Install tools
release:create                Generate release commit
release:batch_changelog       Generate changelog for existing git tags
release:changelog             Generate changelog for an existing version
release:changelog_next        Generate changelog for a new version
release:commit_release        Create release commit
```

## Others

- GitHub Actions for automating releases: https://github.com/ghacts/gitflow

## Contact

Le Minh Tri [@ansidev](https://ansidev.xyz/about).

## License

This source code is available under the [MIT LICENSE](/LICENSE).
