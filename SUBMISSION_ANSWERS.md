# GitHub Actions Security - Submission Answers

## Questions and Answers

### 1. What is the difference between official actions and third-party actions?

**Official Actions:**
- Maintained by GitHub/Microsoft under the `actions/` organization
- Regularly audited and cryptographically signed
- Examples: `actions/checkout@v4`, `actions/upload-artifact@v4`

**Third-Party Actions:**
- Created by community developers under various organizations
- Variable security practices and maintenance
- Examples: `actions-security-demo/harden-runner@main`, `docker/setup-buildx-action@v3`

### 2. Which actions are risky to use and what are the risks?

**Risky Actions:**
- Third-party actions from unknown maintainers
- Actions with broad permissions
- Actions that haven't been updated recently

**Risks:**
- **Supply Chain Attacks**: Malicious code injection
- **Credential Theft**: Access to secrets and tokens
- **Dependency Vulnerabilities**: Outdated or vulnerable dependencies
- **Code Execution**: Actions run with repository permissions
- **Maintenance Issues**: Abandoned or poorly maintained actions

### 3. One-Sentence Explanation

**Why the check failed:** The demo workflow used third-party actions (`actions-security-demo/harden-runner@main` and `docker/setup-buildx-action@v3`) that were not in the approved whitelist, triggering the policy enforcement mechanism.

**How it was fixed:** The disallowed third-party actions were replaced with equivalent functionality using built-in commands and only approved GitHub actions (`actions/checkout@v4` and `actions/upload-artifact@v4`), ensuring compliance with the security policy.

## Files to Submit

1. **Screenshot of failing PR check** - Shows policy violation with disallowed actions
2. **Screenshot of passing PR check** - Shows policy compliance after fix
3. **`restricted.yml` file** - Policy enforcement workflow
4. **One-sentence explanation** - (provided above)

## Expected Results

### Failing PR Check
```
❌ Policy violation: 2 disallowed action(s) found
❌ Line 24: 'actions-security-demo/harden-runner' is not allowed
❌ Line 27: 'docker/setup-buildx-action' is not allowed
```

### Passing PR Check
```
✅ Policy check passed: All 2 action(s) are approved
✅ Line 12: 'actions/checkout' is allowed
✅ Line 15: 'actions/upload-artifact' is allowed
```

## Security Benefits

1. **Supply Chain Protection**: Prevents malicious action usage
2. **Compliance**: Ensures only approved actions are used
3. **Audit Trail**: Tracks all action usage
4. **Risk Reduction**: Eliminates unknown dependencies
5. **Automated Enforcement**: No manual review needed
