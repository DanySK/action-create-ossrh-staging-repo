# Create OSSRH Staging Repository GitHub Action

![Action: Create Staging Repository](https://img.shields.io/badge/Action-Create%20Staging%20Repository-blueviolet?logo=github)

This composite action creates a **Sonatype staging repository** on Maven Central so you can deploy your artifacts. It finds the appropriate profile ID based on your `groupId`, then opens a new staging repository using Sonatype’s Nexus REST API.

## Table of Contents

- [Features](#features)
- [Inputs](#inputs)
- [Outputs](#outputs)
- [Usage](#usage)
- [Example](#example)
- [Contributing](#contributing)
- [License](#license)

---

## Features

- **Automated profile lookup**: Uses your `groupId` to dynamically retrieve the Sonatype staging profile ID.
- **Opens a staging repository**: Creates a new staging repository for Maven Central deployments.
- **Easy integration**: Drop into any workflow to simplify the Maven Central release process.
- **Secure credentials handling**: Expects credentials to be set as GitHub Actions secrets.

---

## Inputs

| Name                      | Description                                                     | Required | Default                |
|---------------------------|-----------------------------------------------------------------|----------|------------------------|
| `group-id`               | The groupId used for the staging repository                     | false    | `org.danilopianini`    |
| `maven-central-username` | Sonatype Username for Maven Central                             | true     | —                      |
| `maven-central-password` | Sonatype Password for Maven Central                             | true     | —                      |

---

## Outputs

| Name               | Description                                         |
|--------------------|-----------------------------------------------------|
| `staging-repo-id` | The ID of the newly created staging repository.      |

---

## Usage

```yaml
jobs:
  staging-repo:
    runs-on: ubuntu-24.04
    steps:
      - name: Create Staging Repository
        id: create-staging-repo
        uses: danysk/action-create-ossrh-staging-repo@1.0.0
        with:
          group-id: "org.danilopianini"
          maven-central-username: ${{ secrets.MAVEN_CENTRAL_USERNAME }}
          maven-central-password: ${{ secrets.MAVEN_CENTRAL_PASSWORD }}
      - name: Use staging repo ID
        run: |
          echo "New staging repository ID is: ${{ steps.create-staging-repo.outputs.staging-repo-id }}"
```
