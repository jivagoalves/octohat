# octohat
[![Build Status](https://travis-ci.org/stackbuilders/octohat.svg?branch=master)](https://travis-ci.org/stackbuilders/octohat)
[![Hackage](https://img.shields.io/hackage/v/octohat.svg)](http://hackage.haskell.org/package/octohat)

A well tested, GitHub API client using `wreq` as a backend

The project uses Stackage to maintain build stability

## Currently supported endpoints

### Members

`module Network.Octohat.Members`

* Add teams to an organization
  `addTeamToOrganization`

* Delete teams from an organization
  `deleteTeamFromOrganization`

* List all members from an organization
  `membersForOrganization`

* List all members from a team, using the team id
  `membersForTeam`

* List all teams from an organization
  `teamsForOrganization`

* Add members to a team
  `addMemberToTeam`

* Delete members from a team
  `deleteMemberFromTeam`

* List Public Keys for a user
  `publicKeysForUser`

## Instructions

### Docker

Requirements:

* [docker](https://docs.docker.com/installation)
* [fig](http://www.fig.sh/install.html)

Build the Docker container:
```
fig up -d
```

Then fire up bash:
```
fig run dev bash
```

You can now run the next instructions to install, build and run tests inside the container. We mount the current directory as `/workspace` so that you only have to install once.

Additionally, if you want to use GHCi:
```
fig run dev
```

Or `cabal repl`:
```
fig run dev cabal repl
```

### To install:
```
cabal sandbox init
cabal install --only-dep --enable-test -jN
```

where N = \<the number of cores in your machine\>

### To build:

```
cabal build
```

### Then run the test suite:

**CAUTION: Use tokens of a test user, not your own account since the test suite clears state on Github before it runs (i.e., it will delete everything in your github account).**

You need to set some environment variables.

Set `SANDBOX_ORGANIZATION` to an organization you don't care about, since the tests will delete all the teams within that organization

Set `TEST_ACCOUNT_ONE` to a test account member of the Owners teams in `$SANDBOX_ORGANIZATION`

Set `TEST_ACCOUNT_TWO` to another test account member of the Owners teams in `$SANDBOX_ORGANIZATION`

Set `TEST_ACCOUNT_THREE` to yet another test account member of the Owners teams in `$SANDBOX_ORGANIZATION`

Set `GITHUB_TOKEN` to an API token from `$TEST_ACCOUNT_ONE`. The token scopes should include full admin privileges and the ability to write public keys.

You can these variables either directly or put them in `.GITHUB_SANDBOX`. Either way they must be set to run the tests. Finally run the tests with:

```
cabal test
```
