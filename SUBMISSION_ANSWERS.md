# GitHub Actions Security - Submission Answers

## Questions & Answers

### What is the difference between official actions and third-party actions?

**Official Actions:**
- Published under the `actions/` organization (e.g., `actions/checkout@v4`)
- Maintained by GitHub/Microsoft teams
- Regularly audited and cryptographically signed
- Generally trusted and secure

**Third-Party Actions:**
- Published by community developers under various organizations (e.g., `actions-security-demo/harden-runner@main`)
- Maintained by individual developers or companies
- Variable security practices and maintenance quality
- Higher risk of supply chain attacks

### Which actions are risky to use?

**Risky Third-Party Actions:**
- Actions from unknown maintainers
- Actions with many dependencies
- Actions that haven't been updated recently
- Actions with broad permissions

**Risks of using risky actions:**
- **Supply Chain Attacks**: Malicious code injection
- **Credential Theft**: Actions can access secrets and tokens
- **Code Execution**: Actions run with repository permissions
- **Dependency Vulnerabilities**: Outdated or vulnerable dependencies
- **Maintenance Issues**: Abandoned or poorly maintained actions

## One-Sentence Explanation

**Why the check failed:** The demo workflow used third-party actions (`actions-security-demo/harden-runner@main` and `docker/setup-buildx-action@v3`) that were not in the approved whitelist, triggering the policy enforcement mechanism.

**How it was fixed:** The disallowed third-party actions were replaced with equivalent functionality using built-in commands and only approved GitHub actions (`actions/checkout@v4` and `actions/upload-artifact@v4`), ensuring compliance with the security policy.

## Files Submitted

1. **Screenshot of failing PR check** - Shows policy violation with disallowed actions
2. **Screenshot of passing PR check** - Shows policy compliance with only allowed actions  
3. **`restricted.yml` file** - Policy enforcement workflow
4. **One-sentence explanation** - Provided above
