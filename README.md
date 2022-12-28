# blocky

To proved that Github green grass("planting grass") means nothing

[![npm version](https://badge.fury.io/js/blocky.svg)](https://badge.fury.io/js/blocky)

- Multiple useful Github utilities based on `Octokit`
- Auto commit, auto cleaning stale workflows, auto cleaning dummy files etc.
- Run cron job using `Github Action`

## How to use

1. create a secret
   Permission to `repo` must be inluded to control workflow

   https://github.com/settings/tokens/new?description=blocky_TOKEN&scopes=repo,read:packages,read:org,delete_repo,workflow

2. set the secret to the target repository

   Go to setting page and set secret as `blocky_TOKEN`

   https://github.com/{OWNER}/{REPO}/settings/secrets/actions

   Make sure that you are the owner of the target repository.

3. initialize blocky and check `./.github/workflows/blocky.yml`

   ```sh
   npx blocky init
   ```

## How to contribute this project

Rename `.env.example` to `.env` and fill the environment values by following instructions.

```sh
# install dependencies
pnpm

# development
pnpm dev

# production
pnpm build
pnpm start
```

## How to make a clean git history

```sh
# interactive rebase and squash all except root commit
# or, git rebase -i HEAD~11
git rebase -i --root

git push origin --force main
```

## clean PR history

```sh
git config pull.rebase true && git pull --prune && git branch -r | grep --only "commit\/167.*" | xargs git push --delete origin && git pull --prune


# git push --delete origin SOME_TAG_NAME
# git tag --delete SOME_TAG_NAME
```

## Roadmap

- [ ] husky, lintstaged, commitizen, commitlint
- [ ] fix the malfunction of `rename stale file`. idea: tree update after set 'sha' as null..
- [ ] how to make user configurable `runner.ts`
- [ ] branch is not configurable now, but should be configurable. currently `main` by default
- [ ] `npx blocky init` does not work and throws error that can't find directory `./.github/workflows/blocky.yml`
- [ ] connect github action with NPM to publish whenever `git push` occurs to specific branch, such as `release` branch