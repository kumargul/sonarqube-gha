# sonarqube-gha

GHA Pipelines for SonarQube

This repository provides GitHub Actions (GHA) pipelines designed to integrate with SonarQube, a popular tool for continuous inspection of code quality and security.

## Features

- Automated code analysis using SonarQube
- Seamless integration with GitHub Actions workflows
- Supports Java (default language)
- Easy to customize and extend for other languages or additional quality gates

## Usage

1. **Clone the repository**  
   ```bash
   git clone https://github.com/kumargul/sonarqube-gha.git
   cd sonarqube-gha
   ```

2. **Configure SonarQube**  
   - Make sure you have access to a SonarQube server.
   - Obtain your SonarQube project key and authentication token.

3. **Set up GitHub Secrets**  
   - In your GitHub repository, go to `Settings > Secrets and variables > Actions`.
   - Add the following secrets:
     - `SONAR_TOKEN`: Your SonarQube authentication token.
     - `SONAR_HOST_URL`: URL of your SonarQube server.

4. **GitHub Actions Workflow**  
   - This repository contains sample workflows to trigger SonarQube analysis on push or pull request.
   - You can modify the workflow files under `.github/workflows/` to fit your project needs.

## Example Workflow

```yaml
# .github/workflows/sonarqube.yml
name: SonarQube Analysis

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

env:
      SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
      SONAR_HOST_URL: ${{ secrets.SONAR_HOST_URL }}

jobs:
  sonarqube:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up JDK 17
        uses: actions/setup-java@v4
        with:
          java-version: '17'
          distribution: 'temurin'
      - name: SonarQube Scan
      uses: SonarSource/sonarqube-scan-action@v2.1.0
      with:
        projectBaseDir: .
        args: >
          -Dsonar.organization=<your-org>
          -Dsonar.projectKey=<your-project>
```

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for improvements.

## License

This project currently does not specify a license.

## Author

- [kumargul](https://github.com/kumargul)

---
Repository: [kumargul/sonarqube-gha](https://github.com/kumargul/sonarqube-gha)