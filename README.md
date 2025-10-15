# Hello World API Specification

## View Packages

You can view all deployed packages at:  
🔗 [GitHub Packages - hello-world-spec](https://github.com/oshmykov-dev/hello-world-spec/packages/)

## Building and Deploying

### Building the Project
```bash
mvn clean install
```

### Deploying
You can deploy the project using either of these methods:

1. Using Maven directly (recommended):
   ```bash
   mvn clean deploy
   ```
   This will automatically use the settings from `.mvn/settings.xml` as specified in the project's `maven.config`.
   
   > **Note about `maven.config` syntax**:
   > - In `maven.config`, the `-s` flag must be directly followed by the path without a space: `-s.mvn/settings.xml`
   > - When running from command line, use a space: `mvn clean -s .mvn/settings.xml deploy`

2. Using IntelliJ IDEA:
   - Open the Maven tool window
   - Click the refresh button to load all Maven projects
   - Navigate to the `deploy` goal under the Lifecycle section and double-click it

   Note: Make sure to configure IntelliJ to use the project's Maven wrapper (mvnw) or a local Maven installation that's properly configured.

This project contains the OpenAPI specification for the Hello World API, packaged as a Maven artifact for easy consumption in other projects.

## Prerequisites

- Java 11 or higher
- Maven 3.6.3 or higher
- GitHub account with access to this repository
- GitHub Personal Access Token (PAT) with `write:packages` scope

### Generating a GitHub Personal Access Token (PAT)

1. Go to your GitHub account settings
   - Click your profile photo in the top-right corner
   - Select **Settings**
   - In the left sidebar, click **Developer settings**
   - Click **Personal access tokens** > **Tokens (classic)**
   - Click **Generate new token** > **Generate new token (classic)**

2. Configure your token:
   - **Note**: Give your token a descriptive name (e.g., "Maven Package Deployment")
   - **Expiration**: Set an expiration date or select "No expiration" (not recommended for security)
   - **Select scopes**: Check the `write:packages` scope (under `repo` section)
   - Click **Generate token**

3. **Important**: Copy the generated token immediately and store it securely. You won't be able to see it again after leaving the page.

4. Configure Maven to use your token by adding it to your Maven settings or environment variables.

## IntelliJ IDEA Setup

### Configuring Maven Settings
1. Open **Preferences/Settings** (⌘, on Mac or Ctrl+Alt+S on Windows/Linux)
2. Navigate to **Build, Execution, Deployment** > **Build Tools** > **Maven**
3. Under **User settings file**, click the folder icon and select the `.mvn/settings.xml` file from your project
4. > **Note**: If you see an **Override** checkbox, you don't need to check it. The `.mvn/settings.xml` will be used automatically by Maven when running from the command line or when the Maven runner is set to use the project settings.
5. Click **Apply** and **OK**

### Setting Environment Variables
1. Open **Run/Debug Configurations** (⌥⇧R on Mac or Shift+F10 on Windows/Linux)
2. Click **Edit Configurations...**
3. In the left panel, select **Maven**
4. Click the **+** button to create a new Maven configuration
5. Name it "Deploy"
6. In the **Command line** field, enter: `clean deploy`
7. Click **Environment variables** (the ... button)
8. Add these variables:
   - `GITHUB_ACTOR` = your GitHub username
   - `GITHUB_TOKEN` = your GitHub Personal Access Token
9. Click **Apply** and **OK**

### Running the Deployment
1. Select your new "Deploy" configuration from the run configurations dropdown
2. Click the green run button (or press ⌃R on Mac or Shift+F10 on Windows/Linux)

## Setup Authentication

Set your GitHub username and token:

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

## Command Line Deployment

### Building Locally
```bash
mvn clean install
```

### Deploying to GitHub Packages
```bash
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
        <groupId>com.example.helloworld</groupId>
        <artifactId>hello-world-spec</artifactId>
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

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

