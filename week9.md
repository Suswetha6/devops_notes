# CI Pipeline — Overview (Kubernetes-ready)

This note summarizes a typical CI pipeline tailored for Java/Maven apps with containerization and Kubernetes deployment. It lists stages, common commands/actions, and short guidance for security and reliability.

## Pipeline stages (concise)

1. Checkout code

   - Action / Command: `actions/checkout` (GitHub Action)
   - Purpose: download repository to the runner for build and test steps.

2. Set up Java & build tools

   - Action / Command: `actions/setup-java` (or install JDK + Maven)
   - Purpose: install JDK, configure Maven; enables dependency caching.

3. Linting / Code quality

   - Command: `mvn checkstyle:check` (or equivalent linting tool)
   - Purpose: enforce style and static quality rules.
   - Notes: consider `continue-on-error: true` only for warnings — prefer failing on real issues.

4. SAST (Static Application Security Testing)

   - Tool: CodeQL (GitHub Code Scanning)
   - Purpose: scan source for common vulnerabilities (OWASP Top 10, patterns).

5. SCA (Software Composition Analysis)

   - Tool: OWASP Dependency-Check, Snyk, or similar
   - Purpose: detect vulnerable third-party libraries and transitive dependencies.

6. Unit testing

   - Command: `mvn test`
   - Purpose: validate business logic; pipeline should fail on test failures.

7. Build application

   - Command: `mvn clean package -DskipTests`
   - Output: JAR/WAR artifact ready for containerization.

8. Build Docker image

   - Command: `docker build -t <registry>/<repo>:<tag> .`
   - Purpose: create an immutable image containing the application.

9. Container image scanning

   - Tool: Trivy, Clair, or similar
   - Purpose: scan base OS and application libraries for CVEs; fail the pipeline on critical/high CVEs.

10. Upload scan results

    - Output format: SARIF or other report formats
    - Purpose: surface security findings in GitHub Security tab or external dashboards.

11. Runtime container test (smoke tests)

    - Steps: `docker run -d -p 8080:8080 <image>` then `curl --fail http://localhost:8080/health` (adjust path)
    - Purpose: verify the container starts and basic endpoints respond.

12. Registry login

    - Action: `docker/login-action` (GitHub Action) or `docker login` using CI secrets
    - Purpose: authenticate to container registry securely using repository secrets.

13. Push image to registry

    - Command: `docker push <registry>/<repo>:<tag>`
    - Purpose: publish the trusted artifact for deployment.

## What happens on code push

- Developer pushes a change to a branch.
- GitHub Actions triggers the CI workflow (runner spins up).
- Build, tests, linters, and security scans run.
- If all checks pass, a Docker image is produced, scanned, smoke-tested, and pushed to the registry.

## Key DevOps & security concepts

- Continuous Integration (CI)
- DevSecOps / shift-left security
- Supply-chain security (SCA, provenance)
- Immutable artifacts (container images)
- Quality gates (tests, scans) that block promotion
- Secrets management (do not hardcode credentials; use GitHub Secrets)
- Infrastructure as Code (IaC) for reproducible deployments

## Why this pattern is industry-grade

- Multi-layer security scanning (SAST, SCA, image scanning)
- Fail-fast on tests or critical vulnerabilities
- Runtime verification (smoke tests before push)
- Secure secret handling and least-privilege actions
- Integration with GitHub security features (SARIF, code scanning)

## Kubernetes + CI/CD (high level)

- CI: builds, tests, and verifies images.
- CD: promotes and deploys images to Kubernetes clusters (via GitOps or pipelines).
- Kubernetes provides scaling, self-healing, rolling/blue-green or canary deployments for zero-downtime updates.

---

Notes / Recommendations:

- Pin action versions (e.g., `actions/checkout@v3`) for stability.
- Use caching (`actions/cache`) for Maven to speed builds.
- Fail on high/critical CVEs; consider warnings for medium/low with triage.
- Store registry credentials and other secrets in GitHub Secrets.
- Consider adding an optional “deploy preview” environment for PRs.
