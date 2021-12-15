# Fetch GH Release Asset

This action downloads an asset from a GitHub release and provides some release details as output. Private repos are supported.
I modify orginally [@dsaltares/fetch-gh-release-asset](https://github.com/dsaltares/fetch-gh-release-asset) to work on composite action insteed docker.

When you use self-hosted github runner in docker, shared directory with workspace doesn't work. So this is why i decade to use composite action.

thx [dsaltares](https://github.com/dsaltares) for orginal bash script!

## Inputs

### `token`

**Required** The GitHub token. Typically this will be `${{ secrets.GITHUB_TOKEN }}`

### `file`

**Required** The name of the file to be downloaded.

### `repo`

The `org/repo` containing the release.

### `version`

The release version to fetch from in the form `tags/<tag_name>` or `<release_id>`. Defaults to `latest`.

### `target`

Target file path. Only supports paths to subdirectories of the GitHub Actions workspace directory

## Outputs

### `version`

The version number of the release tag. Can be used to deploy for example to itch.io

### `name`

[Also called a title of a release](https://docs.github.com/en/github/administering-a-repository/managing-releases-in-a-repository). Defaults to the same value as `version` if not specified when creating a release. 

### `body`

The body (description) of a release.

## Example usage

```yaml
uses: dsaltares/fetch-gh-release-asset@master
with:
  repo: "paweb88/fetch-gh-release-asset"
  version: "tags/v0.1.18"
  file: "plague-linux.zip"
  target: "subdir/plague-linux.zip"
  token: ${{ secrets.GITHUB_TOKEN }}
```

## Support

This action only supports Linux runners as this is a [docker container](https://docs.github.com/en/actions/creating-actions/about-actions#types-of-actions) action. If you encounter `Error: Container action is only supported on Linux` then you are using non-linux runner.
