# 🎯 GitHub Actions Security Demo - Complete Instructions

## ✅ What's Already Done

1. ✅ **Repository Setup**: All files pushed to your GitHub repository
2. ✅ **Initial Commit**: Policy enforcement workflow added to main branch
3. ✅ **Feature Branch**: `feature/demo` branch created with disallowed actions
4. ✅ **Ready for PR**: Branch pushed and ready for pull request

## 🚀 Next Steps (Do These Now)

### Step 1: Create Pull Request (Failing Scenario)

1. **Go to your GitHub repository**: https://github.com/janessa-redalpha/github-actions-security-demo
2. **Click "Compare & pull request"** for the `feature/demo` branch
3. **Create PR** from `feature/demo` to `main`
4. **Wait for the policy check to run** (it should FAIL)
5. **📸 Take a screenshot** of the failing check

**Expected Failing Result:**
```
❌ Policy violation: 2 disallowed action(s) found
❌ Line 21 in .github/workflows/demo.yml: 'actions-security-demo/harden-runner' is not allowed
❌ Line 24 in .github/workflows/demo.yml: 'docker/setup-buildx-action' is not allowed
```

### Step 2: Fix the Workflow (Success Scenario)

**Run these commands in your terminal:**

```bash
cd /home/jnssa/DevSecOps/github-actions-security-demo

# Replace with fixed version
cp .github/workflows/demo-fixed.yml .github/workflows/demo.yml

# Commit the fix
git add .github/workflows/demo.yml
git commit -m "Fix demo workflow to use only allowed actions

Replaced disallowed third-party actions with equivalent functionality:
- Removed actions-security-demo/harden-runner@main
- Removed docker/setup-buildx-action@v3
- Added equivalent functionality using built-in commands
- Now only uses approved actions: actions/checkout@v4 and actions/upload-artifact@v4

Expected result: Policy check should PASS"

# Push the fix
git push origin feature/demo
```

### Step 3: Verify Fix (Success Scenario)

1. **Go back to your GitHub Pull Request**
2. **Wait for the policy check to run again** (it should now PASS)
3. **📸 Take a screenshot** of the passing check

**Expected Passing Result:**
```
✅ Policy check passed: All 2 action(s) are approved
✅ Line 12 in .github/workflows/demo.yml: 'actions/checkout' is allowed
✅ Line 15 in .github/workflows/demo.yml: 'actions/upload-artifact' is allowed
```

## 📸 Screenshots to Capture

### Screenshot 1: Failing PR Check
- Show the policy check failing
- Show the specific disallowed actions
- Show the error message

### Screenshot 2: Passing PR Check  
- Show the policy check passing
- Show the approved actions
- Show the success message

## 📝 One-Sentence Explanation

**Why the check failed:** The demo workflow used third-party actions (`actions-security-demo/harden-runner@main` and `docker/setup-buildx-action@v3`) that were not in the approved whitelist, triggering the policy enforcement mechanism.

**How it was fixed:** The disallowed third-party actions were replaced with equivalent functionality using built-in commands and only approved GitHub actions (`actions/checkout@v4` and `actions/upload-artifact@v4`), ensuring compliance with the security policy.

## 📋 Files to Submit

1. **Screenshot of failing PR check**
2. **Screenshot of passing PR check**
3. **`restricted.yml` file** (already in your repo)
4. **One-sentence explanation** (provided above)

## 🔍 What Each File Does

### `restricted.yml` - Policy Enforcement Workflow
- Scans all workflow files for disallowed actions
- Only allows `actions/checkout` and `actions/upload-artifact`
- Blocks PRs with disallowed actions
- Provides detailed violation reporting

### `demo.yml` - Failing Scenario
- Contains disallowed third-party actions
- Will trigger policy violation
- Demonstrates security risks

### `demo-fixed.yml` - Success Scenario
- Contains only allowed actions
- Will pass policy check
- Shows compliant workflow

## 🎉 Success Criteria

- [ ] ✅ Repository setup complete
- [ ] ✅ Failing PR created and screenshot taken
- [ ] ✅ Workflow fixed to use only allowed actions
- [ ] ✅ Passing PR verified and screenshot taken
- [ ] ✅ One-sentence explanation provided

## 🆘 Need Help?

If you encounter any issues:

1. **Check the GitHub Actions tab** in your repository
2. **Verify the workflow files** are in `.github/workflows/`
3. **Check the YAML syntax** is correct
4. **Ensure the branch** is pushed to GitHub

## 🎯 Quick Commands Reference

```bash
# Check status
git status

# View files
ls -la .github/workflows/

# Check workflow syntax
cat .github/workflows/restricted.yml

# Push changes
git add .
git commit -m "Your message"
git push origin feature/demo
```

You're all set! The repository is ready and the demonstration should work perfectly. 🚀
