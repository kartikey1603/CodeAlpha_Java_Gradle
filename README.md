# CodeAlpha — Java Application using Gradle (Task 3)

A minimal Java application project. 
This project demonstrates a simple CLI Java application that prints "Hello World!" and is built, tested and run using the Gradle Wrapper.

Summary
- Language: Java (JDK 17 toolchain configured)
- Purpose: Educational task to show build, run and test using Gradle
- Main commands used for the internship submission:
  - Build: `./gradlew build`
  - Run: `./gradlew run`
  - Test: `./gradlew test`

Important files
- `app/src/main/java/org/example/App.java`  
  Main application — contains `getGreeting()` and `main()` which prints "Hello World!".
- `app/build.gradle`  
  Gradle build configuration for the `app` project (application plugin + toolchain).
- `settings.gradle`  
  Root settings file including the `app` subproject.
- `gradle/wrapper/*`  
  Gradle wrapper files (use these so no global Gradle install is required).
- `.github/workflows/gradle-cicd.yml` (CI)  
  GitHub Actions workflow that builds the project on pushes/PRs to `main`.
- `gradle/libs.versions.toml`  
  Centralized dependency versions (dependency management).

Prerequisites
- JDK 17 (recommended) or allow Gradle toolchain to download an appropriate JDK (requires network).
- Git (to clone repo).
- No global Gradle installation required — use the included Gradle Wrapper.

Quick start (Unix / macOS / WSL)
1. Clone the repository (if not already):
   ```bash
   git clone https://github.com/kartikey1603/CodeAlpha_Java_Gradle.git
   cd CodeAlpha_Java_Gradle
   ```
2. Build the project:
   ```bash
   ./gradlew build
   ```
   - Output: artifacts and reports will appear under `app/build/` (e.g. `app/build/libs/`).

3. Run the application:
   ```bash
   ./gradlew run --project-dir app
   ```
   - Example printed output:
     ```
     > Task :app:run
     Hello World!
     ```

4. Run tests:
   ```bash
   ./gradlew test --project-dir app
   ```
   - Test reports: `app/build/reports/tests/test/index.html`
   - Console shows test summary; tests use JUnit Jupiter.

Quick start (Windows CMD / PowerShell)
- Use the wrapper script `gradlew.bat` or `.\gradlew`:
  ```powershell
  .\gradlew.bat build
  .\gradlew.bat run --project-dir app
  .\gradlew.bat test --project-dir app
  ```

Notes on the commands
- `./gradlew build`  
  Compiles the code, runs tests, and assembles artifacts.
- `./gradlew run`  
  Runs the application using the `application` plugin's configured `mainClass`.
- `./gradlew test`  
  Executes unit tests (JUnit) and generates test reports.

Where to find outputs
- Compiled JARs: `app/build/libs/`
- Test results: `app/build/test-results/test/`
- Test report (HTML): `app/build/reports/tests/test/index.html`

CI
- The repository includes a GitHub Actions workflow (`.github/workflows/gradle-cicd.yml`) that:
  - Runs the Gradle build on pushes and pull requests to `main`.
  - Uses JDK 17 (Temurin) on `ubuntu-latest`.
  - This provides an automated CI check for build/test on every push/PR.

How this project covers the learning objectives
Below is a short mapping of the Task learning goals to concrete project elements and practices included in this repository.

1) Automate Java project builds using Gradle
- Where: `app/build.gradle`, Gradle Wrapper (`gradlew`, `gradlew.bat`, `gradle/wrapper/*`)
- How: Running `./gradlew build` executes a repeatable, automated build pipeline (compile → test → assemble). The Gradle Wrapper ensures the same Gradle version is used by all evaluators and CI.

2) Manage dependencies efficiently in the Java app
- Where: `gradle/libs.versions.toml` and `app/build.gradle`
- How: Dependency versions are centralized in `gradle/libs.versions.toml` and referenced from `build.gradle`. This makes version updates and auditing easier and keeps dependency declarations consistent.

3) Integrate CI/CD pipelines for continuous delivery
- Where: `.github/workflows/gradle-cicd.yml`
- How: The GitHub Actions workflow runs `./gradlew build` on push and pull requests to `main`. This enforces continuous integration: every change is automatically built and tested, catching regressions early. (To extend toward CD, one could add steps to publish artifacts to a registry or deploy to a test environment.)

4) Streamline build and deployment processes
- Where: Gradle `application` plugin in `app/build.gradle`, wrapper files, and the CI workflow
- How: The `application` plugin simplifies running the app (`./gradlew run`). The Wrapper + CI make building and testing repeatable and scriptable, which streamlines handoffs between development, CI, and potential deployment steps.

5) Understand core DevOps principles in Java development
- Where: All configuration together (`build.gradle`, `settings.gradle`, wrapper, CI)
- How: This project demonstrates several DevOps best practices:
  - Automation: builds, tests and CI are automated (no manual steps required).
  - Reproducibility: Gradle Wrapper pins the Gradle version, and the toolchain config (Java 17) promotes consistent environments.
  - Continuous feedback: CI provides immediate feedback on code changes (build/test results).
  - Traceability & artifacts: build artifacts and test reports are produced in `app/build/`, enabling traceability of what was produced for a given commit.
  - Version control: project configuration and CI are stored in the repository for code review and auditing.

Troubleshooting
- If Gradle wrapper fails to download the distribution, check network or proxy settings.
- If the JDK version is missing, the Gradle toolchain configured in `build.gradle` should download it; otherwise install JDK 17 locally.
- Use `./gradlew --stacktrace <task>` for detailed error output.
