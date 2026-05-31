# Open Source Contributions Tracker

Public log of all OSS contributions — successes, failures, lessons learned.

## Active Contributions

### Circle Ecosystem

#### ✅ circlefin/skills
- **PR #30**: `use-refund-protocol` skill
- **Status**: Submitted, awaiting review
- **Type**: Documentation + code examples
- **Value**: Non-custodial USDC escrow integration guide
- **Link**: https://github.com/circlefin/skills/pull/30
- **Submitted**: 2026-05-31

#### ✅ circlefin/arc-node
- **PR #100**: MetaMask integration guide with USDC token setup
- **Status**: Submitted, awaiting review
- **Type**: Documentation
- **Value**: Unblocks all Arc Testnet DApp developers (fixes #97)
- **Link**: https://github.com/circlefin/arc-node/pull/100
- **Submitted**: 2026-05-31
- **Expected review**: 1-2 days (based on recent doc PRs)

#### ⏳ circlefin/malachite
- **Issue #1529**: Replace panics with typed errors in discovery crate
- **Status**: Assignment requested
- **Type**: Bug fix (production reliability)
- **Value**: Prevents process crashes on misconfiguration
- **Link**: https://github.com/circlefin/malachite/issues/1529
- **Requested**: 2026-05-31

- **Issue #1106**: Split HostMsg enum into separate crate
- **Status**: Assignment requested
- **Type**: Refactoring (good-first-issue)
- **Value**: Better crate boundaries, API design
- **Link**: https://github.com/circlefin/malachite/issues/1106
- **Requested**: 2026-05-31

## Pipeline

### High Priority
1. **arc-node #97**: Document wallet_watchAsset for USDC in MetaMask
   - Fast review cycle (1-2 days)
   - Unblocks all Arc Testnet developers
   - Low complexity

2. **buidl-wallet-contracts #111**: Security fix in ColdStorageAddressBookModule
   - Critical security bug
   - One-line fix + test
   - Slow review cycle (weeks)

## Lessons Learned

### 2026-05-31: Validate Before Submitting
**Context**: Submitted `use-refund-protocol` skill PR without testing code examples.

**Discovery**: README contains security warning about arbiter drain vulnerability in `earlyWithdrawByArbiter()` function.

**Impact**: Skill documents vulnerable contract. Need to update PR with security warnings.

**Lesson**: Always test code examples and verify contract security before documenting. Documentation without validation = noise.

### 2026-05-31: Follow Project Workflows
**Context**: Attempted to contribute to malachite without understanding contribution policy.

**Discovery**: Malachite requires issue assignment BEFORE submitting PRs. Rejects unsolicited work.

**Impact**: Must wait for maintainer approval before implementing.

**Lesson**: Read CONTRIBUTING.md first. Respect project workflows even when eager to contribute.

### 2026-05-31: Value Over Volume
**Context**: Initially planned to implement multiple documentation skills in parallel.

**Realization**: Documentation without real-world validation doesn't bring value. Better to fix bugs, test existing code, or solve technical problems.

**Lesson**: Prioritize contributions that solve real problems over incremental documentation.

## Contribution Philosophy

### What Brings Value
- Bug fixes with clear reproduction steps
- Security fixes
- Performance improvements with profiling data
- Missing features with clear specs
- Documentation that fills real gaps (not just adding words)

### What Doesn't
- Documentation theater (writing docs without testing)
- Style/formatting PRs without substance
- Premature abstractions
- Unsolicited refactoring

## Stats

- **PRs Submitted**: 2
- **Issues Requested**: 2
- **Merged**: 0 (pending)
- **Rejected**: 0
- **In Review**: 2

---

Last updated: 2026-05-31
