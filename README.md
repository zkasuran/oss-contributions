# Open Source Contributions Tracker

Public log of all OSS contributions — successes, failures, lessons learned.

## Active Contributions

### Circle Ecosystem

#### circlefin/skills
- **PR #30**: `use-refund-protocol` skill
- **Status**: Open, awaiting maintainer review (mergeable, branch protection blocked on required reviews)
- **Type**: Documentation + code examples
- **Value**: Non-custodial USDC escrow integration guide
- **Link**: https://github.com/circlefin/skills/pull/30
- **Submitted**: 2026-05-31
- **Note**: A non-maintainer left an approving review; the required review count is still unmet, so this is not yet review-approved.

#### circlefin/arc-node
- **PR #100**: MetaMask integration guide with USDC token setup
- **Status**: Open, awaiting maintainer review. Updated 2026-06-09 with correctness fixes.
- **Type**: Documentation
- **Value**: Unblocks Arc Testnet DApp developers (addresses #97)
- **Link**: https://github.com/circlefin/arc-node/pull/100
- **Submitted**: 2026-05-31
- **Update 2026-06-09**: A community comment (#89) prompted a re-verification of the guide against the repo config, the MetaMask spec and the live testnet RPC. Found and fixed three real defects in the original guide: wrong chainId (`0x4CF252` = 5042770, should be `0x4CEF52` = 5042002), wrong nativeCurrency (`USDC`/6 decimals, MetaMask requires `ETH`/18 per #95), and a dead RPC URL (`rpc.arc.network`, switched to `rpc.drpc.testnet.arc.network`, #90). Also documented the `wallet_switchEthereumChain` silent-fail workaround (#89).

- **PR #127**: CCTP V2 integration guide for Arc Testnet
- **Status**: Open, awaiting maintainer review. Submitted 2026-06-09.
- **Type**: Documentation (resolves #110)
- **Value**: Documents the Arc-specific CCTP V2 details (domain 26, V2-only depositForBurn selector, minFinalityThreshold 2000, gas-estimation workaround, Iris attestation flow) for every developer moving native USDC on and off Arc.
- **Link**: https://github.com/circlefin/arc-node/pull/127
- **Verification**: domain + contract addresses checked against Circle's CCTP references; both depositForBurn selectors computed via keccak (V2 `0x8e0250ee`, V1 `0x6fd3504e`); TokenMessenger confirmed to have code on Arc Testnet via `eth_getCode`; Iris API paths confirmed live.
- **Note**: chosen after a deep review of arc-node established that the flashy bug reports (#59, #87, #111, #57) all trace to upstream reth or live infra, and Arc's own Rust + Solidity is well-defended (two security sweeps, zero exploitable findings). A verified docs gap was the honest high-value contribution available.

### Base Network

#### base/docs
- **PR #1559**: Security fix for SIWE authentication examples
- **Status**: Open, awaiting maintainer review (0/2 required reviews, no human activity since submission)
- **Type**: Security fix
- **Value**: Prevents cross-domain replay attacks in authenticate-users guide
- **Link**: https://github.com/base/docs/pull/1559
- **Submitted**: 2026-05-31
- **Severity**: High (affects developers following the auth tutorial)

- **PR #1560**: Replace Math.random() with crypto.randomUUID() for SIWE nonces
- **Status**: Open, awaiting maintainer review (0/2 required reviews, no human activity since submission)
- **Type**: Security fix
- **Value**: Fixes predictable nonce generation in 4 documentation examples
- **Link**: https://github.com/base/docs/pull/1560
- **Submitted**: 2026-05-31
- **Severity**: High (enables replay attacks)

#### base/account-sdk
- **PR #335**: Throw error instead of warning for test-only function in production
- **Status**: Open, awaiting maintainer review (0/1 required reviews, no human activity since submission)
- **Type**: Production safety fix
- **Value**: Prevents accidental misuse of a test utility that could drain token allowances
- **Link**: https://github.com/base/account-sdk/pull/335
- **Submitted**: 2026-05-31
- **Severity**: Medium (production safety)

## Closed / Not Pursued

#### circlefin/malachite (issue assignments not granted)
- **Issue #1529**: Replace panics with typed errors in discovery crate
  - Requested assignment 2026-05-31. The maintainer had already `/assign`ed the issue to another contributor (giwaov, 2026-04-09) before the request. Not pursuing.
  - Link: https://github.com/circlefin/malachite/issues/1529
- **Issue #1106**: Split HostMsg enum into separate crate
  - Requested assignment 2026-05-31. The maintainer had already `/assign`ed the issue to another contributor (naijauser, 2026-03-13) and signalled an existing PR was in flight. Not pursuing.
  - Link: https://github.com/circlefin/malachite/issues/1106
- **Lesson**: Check the issue timeline for an existing `/assign` before requesting assignment. Both of these were already taken.

## Pipeline

### High Priority
1. **arc-node #97**: Document wallet_watchAsset for USDC in MetaMask
   - Addressed by PR #100 (now also covers #89, #90, #95)

2. **buidl-wallet-contracts #111**: Security fix in ColdStorageAddressBookModule
   - Critical security bug
   - One-line fix + test
   - Slow review cycle (weeks)

## Lessons Learned

### 2026-06-09: Verify Your Own Doc Before Defending It
**Context**: A community comment on arc-node #100 suggested adding a `wallet_switchEthereumChain` note.

**Discovery**: Re-checking the whole guide against the repo config, the MetaMask spec and the live RPC turned up three real defects in the original PR: a transposed chainId, a nativeCurrency config MetaMask would reject, and a dead RPC URL.

**Impact**: The original guide was documentation that would not actually work if a developer copy-pasted it. Fixed all three plus the suggested addition.

**Lesson**: A doc PR is only valuable if every value in it is verified. Run the calls, hit the endpoints, check the numbers against the source of truth, not just once at write time but again when anyone questions any part of it.

### 2026-05-31: Validate Before Submitting
**Context**: Submitted `use-refund-protocol` skill PR without testing code examples.

**Discovery**: README contains security warning about arbiter drain vulnerability in `earlyWithdrawByArbiter()` function.

**Impact**: Skill documents vulnerable contract. Need to update PR with security warnings.

**Lesson**: Always test code examples and verify contract security before documenting. Documentation without validation = noise.

### 2026-05-31: Follow Project Workflows
**Context**: Attempted to contribute to malachite without understanding contribution policy.

**Discovery**: Malachite requires issue assignment BEFORE submitting PRs, and the issues were already assigned to others.

**Impact**: No path to contribute on those issues.

**Lesson**: Read CONTRIBUTING.md first, and check the issue timeline for an existing assignment before requesting.

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
- Documentation that fills real gaps (verified against the source of truth)

### What Doesn't
- Documentation theater (writing docs without testing)
- Style/formatting PRs without substance
- Premature abstractions
- Unsolicited refactoring

## Stats

- **PRs Submitted**: 6
- **Issues Requested**: 2 (both already assigned to others, not pursued)
- **Merged**: 0
- **Rejected**: 0
- **In Review**: 6 (all mergeable, blocked on maintainer review)
- **Security Fixes**: 3
- **Production Safety**: 1
- **Documentation**: 3

---

Last updated: 2026-06-09
