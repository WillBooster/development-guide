---

# Development Guide

This document compiles guidance for developers who are new to WillBooster.

## Introduction

All projects use [Git](https://git-scm.com/). If you have no experience using it, please learn how to use it beforehand.

In many projects, we primarily adopt the following languages and frameworks. Reading introductory articles and tutorials to gain a certain understanding before starting development will help you proceed smoothly.

- [TypeScript](https://www.typescriptlang.org/)
- [React](https://react.dev/)
- [Next.js](https://nextjs.org/)
- [Prisma](https://www.prisma.io/)

## Development Environment

Please refer to [Introduction to Development](introduction_to_development.md) (Japanese only).

## Operation Confirmation

In most projects, you can perform basic operation checks with the following common command. There are exceptions, so if it does not work, please contact the project manager.

You can start the application in development mode with the following command. To see the result, open http://localhost:3000 in your browser.

```sh
yarn start
```

If you are running the application for the first time, please execute the following command in advance. The seed data includes users for operation checks, and you can sign in with the username and password described in `db/seeds/index.ts`.

```sh
# Install dependency packages.
yarn

# Initialize the database.
yarn db-reset
```

You can easily check the state of the database by starting Prisma Studio with the following command.

```sh
yarn run prisma studio
```

You can run tests with the following command.

```sh
yarn test
```

## Development Flow

At WillBooster, tasks are managed using GitHub issues. In-house developers assign tasks by setting assignees for each issue.

1. Fetch the latest source code and reflect the latest DB schema
   ```
   git pull
   yarn db-migrate
   ```
2. Check the assigned issue from GitHub issues
   - If you want to work on an unassigned issue, such as when there are no assigned issues, get permission from Code Owners.
   - Code Owners may not notice when issues are running low, so be proactive in reaching out 💪.
3. Decide on one issue to work on and create a branch dedicated to that issue
   - There is no strict rule for naming branches, but if you have no particular preference, `<issue number>-<brief description of change>` (e.g., `34-problems-page`) is recommended.
   - e.g., `git switch -c 34-problems-page`
4. Make some changes and commit
   - There are rules for writing PR titles, as in step 7, but there are no rules for commit messages.
   - The granularity of commits is also up to you, but it's safer and easier to roll back if you keep detailed records.
   - e.g., `git add -A && git commit -m "Implementing problems page"`
   - If you cannot commit due to Linter errors, add `--no-verify`.
5. Even if it's not complete, push the created branch to the remote repository (GitHub)
   - e.g., `git push origin 34-problems-page`
   - If you cannot push due to type errors, add `--no-verify`.
     - Try `yarn gen-code` as well, as not running framework code generation could be the cause.
6. Create a Pull request (PR) for the corresponding branch on GitHub.
   - Creating a PR early makes it easier for other developers to offer advice.
7. Comply the PR title with [Conventional Commits](https://www.conventionalcommits.org/ja/v1.0.0/).
   - At the beginning of the PR title, add `feat:` for new features or improvements, `fix:` for bug fixes, `test:` for adding, improving, or fixing tests, etc.
   - The PR title becomes the commit message when merged into the `main` branch.
   - Since it's merged using Squash & Merge, individual commits do not need to follow Conventional Commits (though they can).
   - If it's unfinished or work in progress, add `[WIP] ` at the beginning of the PR title.
     - Example: `[WIP] feat: implement the problems page`
8. Repeat changes, commits, and pushes
9. Once completed, request a review from other developers.
   - If the PR title includes `[WIP]`, remove it.
   - Add a `review requested` label to the PR.
   - Assign one developer working on similar tasks as a reviewer if none are available, assign one of the Code Owners.
   - In the PR comments, mention all Code Owners and the assigned reviewer to request a review.
10. If the reviewer points out any issues, make changes, commit, and push
11. Once you have addressed the feedback, request a re-review (refer to the diagram below for the request method)
    ![image](https://user-images.githubusercontent.com/436237/152084294-0f0b332d-2f75-4daf-b7e4-2b3ab8d61333.png)
12. Once you receive Approval from Code Owners, the issue is considered complete
13. Merge the PR only if instructed by Code Owners. Do not merge without instruction.
    - This is because there may be cases where it's desirable to delay merging for project progression reasons.

## Q&A

### Database Backup Method (For Internal Developers Only)

1. Download the attachment `gcp-sa-key.json (<project name>)` from Bitwarden.
2. Rename the file you downloaded in step 1 to `gcp-sa-key.json` and place it in the root directory of this repository.
3. Execute the command `WB_ENV={staging or production} yarn db-restore` to obtain a backup.
   - The backup file will be generated in `db/restored.sqlite3`. Be aware that if a file with the same name already exists, it will be overwritten.

## Troubleshooting

### Unable to open http://localhost:3000.

This explanation targets individuals who meet the following conditions:

- **Using WSL2 and have set a memory limit.**  
  There's a possibility that the operation is very slow due to having set the memory limit for WSL too low. Please try the following steps:
  1. Display system resources to check the memory usage of WSL. If the memory usage of WSL does not nearly match the limited memory, then the memory limit is not the cause.
  2. Change the settings of the wslconfig file that limits memory to increase the memory size limit of WSL.

### Type errors occur in code that should not have any issues after pulling changes

Please try executing the following command:

```
yarn gen-code
```