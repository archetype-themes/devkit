# Theme Release Workflow + Automations

In this document, we'll walk through the theme development workflow and the automations that support it. We'll cover the following topics:

- Overview of theme development workflow
- Branch strategy overview
- Release process steps
- Store-specific branch management
- Automated workflows (e.g., theme-release-please.yml)
- Post-release actions and maintenance

## General Approach

We've landed on a [Gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) based approach to theme development that is centered around the **develop** and **main** branches, alongside branches that are linked to stores via the Shopify Github Integration. The general approach to developing themes is as follows:

1. Make your changes in `develop` and merge them into `main` when you're ready to release
2. QA `main` on your own persoanl dev store or via linked stores branches (ie. `*/main`)
3. Merge the automatically generated [release-please](https://github.com/googleapis/release-please) PR to trigger release automations and publish a new release
4. Merge each automatically generated linked store PRs to publish release to */production of that store

## Branch Strategy

Our branches maintain a clear seperation between uncustomized theme code and theme code linked to stores that contain theme editor customizations and custom code customizations. This separations assists in isolating customizations and ensures a smooth development, QA, and release process.

### Uncustomized Theme Code Branches

These branches contain theme code in a default state that has not been installed on a store and customized.

`main`:
- Contents ready to package and submit to Theme Store
- Represents a clean, unedited theme package without any theme editor customizations applied

`develop`:
- Contains all unreleased feature branches that will be included in the next release
- Can include unreleased version of components
- Feature branches can be branched and merged into this branch as needed
- Merged into `main` when a new release is ready

`feature/*`
- Branched from `develop` and merged back into `develop` when feature is tested ready

`hotfix/*`
- Branched from `main` and merged back into `main` and `develop`

### Store-specific Branches

These branches contain theme code that are linked to a particular store via the Shopify Github Integration, have been customized in the theme editor and can include custom code. The `*` in these branch names corresponds to a given store name or identifier.

`*/main`
- Remains automatically synced with `main` except for theme editor configuration, ie. settings_data.json, sections/\*.json, template/*.json
- Remains as an unpublished theme. Used to preview what `main` currently looks like on a particular store.

`*/develop`
- Remains automatically synced with `develop` except for theme editor configuration, ie. settings_data.json, sections/\*.json, template/*.json
- Remains as an unpublished theme. Used to preview what `develop` currently looks like on a particular store.

`*/staging`
- Staging branch used to hold and preview the latest release before merging into `*/production`
- Allows for changes to continue to be pushed to main while we wait for latest release to be published on Theme Store
- Allows for any final theme editor customizations that need to be done before merging `*/production`

`*/production`
- Production branch that is the published theme on a store
- Theme Editor customizations performed on `*/production` via Shopify Admingenerate a PR to be merged into `*/main` which will also block a release PR from being merged until it's resolved. This makes sure that Theme Editor customizations are not lost when a new release is published.

## Actions

We depend on a few CI automations implemented via Github Actions to streamline and support our theme development workflow.

### merge-main-branches.yml

[Link to workflow file](https://github.com/archetype-themes/reference-theme/blob/main/.github/workflows/merge-main-branches.yml)


Ensures that `main` + `*/main` and `develop` + `*/develop` branches always remain in sync, while persisting the linked store's theme editor customizations.

Outcomes:
- Makes sure that there is always a preview of `main` available on each store
- Allows you to easily QA `main` on stores before creating a release
- Allows you to develop a feature and preview it in existing stores

Steps:
- Triggered on push to `main`
- Merge changes from `main` into each `*/main` branch
- Persist (don't change) the theme editor config files that already exist in `*/main`, ie. `templates/*.json`, `sections/*.json`, `config/settings_data.json`
- If merge cannot be done automatically, a PR is opened so conflicts can be resolved


### theme-release-please.yml

[Link to workflow file](https://github.com/archetype-themes/reference-theme/blob/main/.github/workflows/theme-release-please.yml)

The core of our automated release and publishing automation is powered by [release-please](https://github.com/googleapis/release-please). This tool automates version management and changelog generation based on conventional commits, streamlining our release process and ensuring consistency across our projects.

Outcomes:
- Create a new release by merging an automatically generated PR
- Update demo shops with latest version by merging an automatically generated PR
- Easy access to theme zip for uploading to Shopify Theme Store + Theme Updater App
- Automatically update our CHANGELOG.md

Steps:
- Creates Pull Request that when merged triggers the release flow
- Bumps repo version based on contents of commits that follow [conventional commit] pattern, ie. breaking, feature, patch
- Bumps version in project files, such as settings_schema.json
- Updates CHANGELOG.md based on contents of conventional commits
- Creates a published Github release when release PR is merged
- Uploads theme zip generated from `shopify theme package` to Github release
- Creates PRs to push latest release to \*/production branches 

### check-release-notes.yml

[Link to workflow file](https://github.com/archetype-themes/reference-theme/blob/main/.github/workflows/check-release-notes.yml)

If you're releasing to the Shopify themes store, than you need to include release notes as a file in your release. This workflow is a check that runs on release-please PRs that checks the `release-notes.md` file to make sure it exists and that it's contents are different from the previous release.

Outcomes:
- Makes sure that we don't forget to update `release-notes.md` before published a release

Steps:
- Looks at the contents of `release-notes.md` from the last tag, and fails if the contents have not changed in a commit since

### check-blocking-prs.yml

[Link to workflow file](https://github.com/archetype-themes/reference-theme/blob/main/.github/workflows/check-blocking-prs.yml)

A check that runs on release-please PRs that checks if an PRs with `autorelease:blocking` are open. If so, the check fails and prevents a new release from being published. Used in conjunction with `open-pr-for-production-changes.yml` to ensure that we handle + preview changes in production before proceeding with a new release.

Outcomes:
- Makes sure that we handle + previews changes in from production before proceeding with a new release

### open-pr-for-production-changes.yml

[Link to workflow file](https://github.com/archetype-themes/reference-theme/blob/main/.github/workflows/open-pr-for-production-changes.yml)

If someone customizes the published theme in the theme editor which is linked via the `*/production` branch, these changes are synced to the associated `*/production` branch as commits via the Shopify Github Integration. We might want these edits to persist when the next release happens, so a PR is created to merge these customizations into the associated `*/main` branch for that particular store.

Outcomes:
- Makes sure that theme editor or code customizations made between releases don't get lost or erased when the next release is pushed to production
- Generates a PR with `autorelease:blocking` label which will block release-please PRs until production customizations are merged into `*/main` or the PR is closed.

Steps:
- Triggered on push to any `*/production` branch
- Create a PR that merges any new commits from `*/production` into the associated `*/main` branch


