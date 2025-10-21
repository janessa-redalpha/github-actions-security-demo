# GitHub Actions Security Policy Enforcement Demo

This repository demonstrates how to enforce security policies for GitHub Actions by automatically scanning and blocking disallowed actions in pull requests.

## Overview

### Official vs Third-Party Actions

**Official Actions** are maintained by GitHub and Microsoft, published under the `actions/` organization:
- **Source**: GitHub's official repositories (github.com/actions)
- **Maintainer**: GitHub/Microsoft teams with dedicated security resources
- **Security**: Generally trusted, regularly audited, cryptographically signed releases
- **Examples**: `actions/checkout@v4`, `actions/upload-artifact@v4`

**Third-Party Actions** are created by the community, published under various organizations:
- **Source**: Individual developers, companies, open-source projects
- **Maintainer**: Community members with varying reliability and security practices
- **Security**: Variable trust level, potential supply chain risks
- **Examples**: `actions-security-demo/harden-runner@main`, `docker/setup-buildx-action@v3`

### Security Risks of Third-Party Actions

1. **Supply Chain Attacks**: Malicious code injection through compromised actions
2. **Dependency Vulnerabilities**: Outdated or vulnerable dependencies
3. **Credential Theft**: Actions can access secrets, tokens, and environment variables
4. **Code Execution**: Actions run with repository permissions and can execute arbitrary code
5. **Maintenance Issues**: Abandoned or poorly maintained actions
6. **Permission Escalation**: Actions can request elevated permissions

## Policy Enforcement

### Allowed Actions (Whitelist)
Only these actions are permitted:
- `actions/checkout`
- `actions/upload-artifact`

### Workflow Files

1. **`restricted.yml`** - Policy enforcement workflow that:
   - Scans all workflow files for disallowed actions
   - Blocks PRs with disallowed actions
   - Provides detailed violation reporting

2. **`demo.yml`** - Failing workflow example with disallowed actions:
   - `actions-security-demo/harden-runner@main` (DISALLOWED)
   - `docker/setup-buildx-action@v3` (DISALLOWED)

3. **`demo-fixed.yml`** - Compliant workflow example with only allowed actions

## Demonstration Flow

### Step 1: Initial Setup
```bash
# Clone and setup
git clone https://github.com/janessa-redalpha/github-actions-security-demo.git
cd github-actions-security-demo
git add .
git commit -m "Add policy enforcement workflow"
git push origin main
```

### Step 2: Create Failing Branch
```bash
# Create feature branch with disallowed actions
git checkout -b feature/demo
cp .github/workflows/demo.yml .github/workflows/demo.yml
git add .github/workflows/demo.yml
git commit -m "Add demo workflow with disallowed actions"
git push origin feature/demo
```

### Step 3: Open Pull Request
- Create PR from `feature/demo` to `main`
- The policy check should **FAIL** due to disallowed actions
- Screenshot the failing check

### Step 4: Fix the Workflow
```bash
# Replace with fixed version
cp .github/workflows/demo-fixed.yml .github/workflows/demo.yml
git add .github/workflows/demo.yml
git commit -m "Fix demo workflow to use only allowed actions"
git push origin feature/demo
```

### Step 5: Verify Fix
- The policy check should now **PASS**
- Screenshot the passing check

## Expected Results

### Failing PR Check
```
❌ Policy violation: 2 disallowed action(s) found
❌ Line 21 in .github/workflows/demo.yml: 'actions-security-demo/harden-runner' is not allowed
❌ Line 24 in .github/workflows/demo.yml: 'docker/setup-buildx-action' is not allowed
```

### Passing PR Check
```
✅ Policy check passed: All 2 action(s) are approved
✅ Line 12 in .github/workflows/demo.yml: 'actions/checkout' is allowed
✅ Line 15 in .github/workflows/demo.yml: 'actions/upload-artifact' is allowed
```

## Security Benefits

1. **Supply Chain Protection**: Prevents malicious action usage
2. **Compliance**: Ensures only approved actions are used
3. **Audit Trail**: Tracks all action usage
4. **Risk Reduction**: Eliminates unknown dependencies
5. **Automated Enforcement**: No manual review needed

## One-Sentence Explanation

**Why the check failed:** The demo workflow used third-party actions (`actions-security-demo/harden-runner@main` and `docker/setup-buildx-action@v3`) that were not in the approved whitelist, triggering the policy enforcement mechanism.

**How it was fixed:** The disallowed third-party actions were replaced with equivalent functionality using built-in commands and only approved GitHub actions (`actions/checkout@v4` and `actions/upload-artifact@v4`), ensuring compliance with the security policy.
