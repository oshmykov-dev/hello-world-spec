# Hello World API Specification

This project contains the OpenAPI specification for the Hello World API, packaged as a Maven artifact for easy consumption in other projects.

## Prerequisites

- Java 11 or higher
- Maven 3.6.3 or higher
- GitHub account with access to this repository
- GitHub Personal Access Token with `write:packages` scope

## Setup Authentication

1. Create a Personal Access Token (PAT) on GitHub with `write:packages` scope
2. Set your GitHub username and token:

### Windows (Command Prompt)
```cmd
set GITHUB_ACTOR=your_github_username
set GITHUB_TOKEN=your_github_token
```

### Windows (PowerShell)
```powershell
$env:GITHUB_ACTOR="your_github_username"
$env:GITHUB_TOKEN="your_github_token"
```

### Mac/Linux (Terminal)
```bash
export GITHUB_ACTOR=your_github_username
export GITHUB_TOKEN=your_github_token
```

## Building and Deploying

```bash
# Build locally
mvn clean install

# Deploy to GitHub Packages
mvn -s .mvn/settings.xml clean deploy
```

## CI/CD Integration

For GitHub Actions, add this step to your workflow:

```yaml
- name: Deploy to GitHub Packages
  run: mvn -s .mvn/settings.xml clean deploy
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Using in Another Project

Add this to your project's `pom.xml`:

```xml
<repositories>
    <repository>
        <id>github</id>
        <url>https://maven.pkg.github.com/oshmykov-dev/hello-world-spec</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>com.example</groupId>
        <artifactId>hello-world-api-spec</artifactId>
        <version>1.0.0-SNAPSHOT</version>
    </dependency>
</dependencies>
```

## Project Structure

```
src/main/resources/api/
  └── openapi.yaml    # OpenAPI specification file
```

## Versioning

To create a new version:

1. Update the version in `pom.xml`
2. Commit your changes
3. Create and push a new tag:
   ```bash
   git tag -a v1.0.0 -m "Version 1.0.0"
   git push origin v1.0.0
   ```

The GitHub Actions workflow will automatically publish the new version to GitHub Packages.

## License

MIT
