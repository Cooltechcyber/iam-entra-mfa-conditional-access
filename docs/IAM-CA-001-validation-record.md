# IAM-CA-001 — Validation Record

**Type:** Simulated IAM security validation case

| Check | Expected | Observed | Outcome |
|---|---|---|---|
| Cloud-only account | Dedicated enabled test identity | Kevin Mitchell; on-premises sync No | Pass |
| Baseline authentication methods | Establish registration state | No usable methods shown | Pass |
| Authenticator registration | Usable MFA method | Microsoft Authenticator, iPhone | Pass |
| Policy assignment | Kevin Mitchell only | Exactly one included user: Kevin Mitchell | Pass |
| Grant control | Require MFA | Grant access + Require multifactor authentication | Pass |
| Initial policy state | Report-only | Report-only shown | Pass |
| Report-only sign-in | Evaluate policy without enforcing | User and resource matched; User action required | Pass |
| Enabled policy | Scoped enforcement | Operator reported policy enabled; later CA result Success | Pass |
| Authentication result | MFA requirement satisfied | Previously satisfied; succeeded true | Pass |
| Fresh MFA prompt | Optional additional verification | Not demonstrated by selected sign-in | Not tested |

## Evidence interpretation
**Report-only: User action required** is a simulated enforcement outcome, not proof that the report-only policy challenged the user.

**Conditional Access: Success** in the later sign-in indicates the policy requirements were met for that event. Authentication Details reported **Previously satisfied**, so this record must not be described as a fresh Microsoft Authenticator push.

## Closure
The lab meets its scoped objective: configure MFA, validate report-only behavior, enable a test-user policy, and corroborate the enforced-policy result using sign-in logs. No production authorization or real-world ticket closure is implied.
