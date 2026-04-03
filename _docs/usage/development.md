---
title: Tool Development
parent: Usage
has_children: false
nav_order: 30
---

## Tool suite development

You should always start a new tool suite by copying the MDI tool suite template.

These links provide detailed descriptions of how to use the template 
and support frameworks to quickly create your own tools:

- <{{ "/mdi-suite-template" | absolute_url  }}>
- <{{ "/mdi-pipelines-framework" | absolute_url  }}>
- <{{ "/mdi-apps-framework" | absolute_url  }}>

The following are additional things to consider and know as you work.

### Create developer-forks of repositories (optional)

The MDI encourages 'fork-and-pull' code development, wherein you 
- fork repositories you need to edit to create "developer-forks"
- edit code in your forks
- make a pull request to the definitive repositories

Most users will only fork their own or their group's repositories,
but you are welcome to fork the MDI frameworks if you
would like to contribute to the MDI codebase.

Forking is not strictly necessary for repos you own, i.e.,
you can edit and push directly to your definitive repo,
but you must fork the MDI frameworks to contribute to them.

### Use the developer flag

Importantly, when developing code you should always include
the `-d` (developer) flag immediately after the CLI alias
at the command line, e.g., `mdi -d ...`. This will use
code either from your cloned developer-fork of all repos,
or place you at the tip of the main branch when you don't have a fork.

For app development, the MDI Desktop has a checkbox
to request a similar developer mode for a running apps server.

### Provide GitHub credentials for private repositories

You can develop and use a private GitHub tool suite repository if you provide a 
[GitHub Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)
(PAT) in a file in your home directory with user-only permissions as follows:

```R
# ~/gitCredentials.R
gitCredentials <- list(
    USER_NAME  = "First Name",
    USER_EMAIL = "namef@umich.edu",
    GIT_USER   = "xxx",
    GITHUB_PAT = "xxx"
)
```

The mdi-manager will read this file to authorize calls to GitHub
when pulling repositories.
