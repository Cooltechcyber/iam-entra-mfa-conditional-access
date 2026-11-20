# IAM-CA-001 — MFA and Conditional Access Security Validation

## Scenario
A fictional cloud-only user, Kevin Mitchell (Security Analyst, Information Technology), was used to validate Microsoft Entra ID MFA registration and a user-scoped Conditional Access policy. This is a controlled training lab, not a production deployment or real service ticket.

## Objectives
- Establish the initial authentication-method baseline.
- Register Microsoft Authenticator for the test identity.
- Configure a policy requiring MFA for the test user.
- Validate policy matching in report-only mode before enforcement.
- Enable the scoped policy and examine sign-in and authentication logs.

## Environment and scope
- Platform: Microsoft Entra ID, cloud-only user
- Test identity: Kevin Mitchell
- Authentication method: Microsoft Authenticator registered on an iPhone
- Licensing: Microsoft Entra ID P2 assignment reported by the lab operator; screenshot 06 is designated as supporting evidence
- Conditional Access policy: `CA-LAB-Require-MFA-KevinMitchell`
- Assignment: Kevin Mitchell only
- Target resources: All resources
- Grant: Grant access, Require multifactor authentication
- Conditions: None configured

## Procedure and observations
1. Inspected the Conditional Access and authentication-method policy baselines.
2. Confirmed the test account was enabled, had the Security Analyst job title and Information Technology department, and was not synchronized from on-premises AD.
3. Observed no usable authentication methods on the test user's initial authentication-method page (hidden or temporary methods were not displayed).
4. Registered Microsoft Authenticator. The user page subsequently showed Microsoft Authenticator (iPhone) as usable, with Authenticator notification as the default sign-in method.
5. Created the scoped MFA policy in **Report-only** mode.
6. Reviewed an interactive sign-in. The **Report only** tab showed the policy, MFA grant control, and **Report-only: User action required**. Detailed evaluation showed user Kevin Mitchell and resource Azure Resource Manager both **Matched**.
7. Verified the selected user scope and the MFA grant control before enforcement.
8. Enabled the policy for the dedicated test user. The operator reported saving the enabled-policy screenshot.
9. Examined a later interactive sign-in. The **Conditional Access** tab showed the MFA policy with **Success**.
10. Inspected **Authentication Details** for that sign-in: authentication method **Previously satisfied**, succeeded **true**, and result indicating the MFA requirement was satisfied.

## Findings
- **PASS — Registration:** Microsoft Authenticator is registered and usable.
- **PASS — Report-only evaluation:** The policy matched the user/resource and indicated further user action would be required.
- **PASS — Enabled-policy result:** Conditional Access showed Success for the MFA policy.
- **PASS — Authentication requirement:** The selected event recorded MFA requirement satisfied via a previously satisfied authentication claim.
- **NOT TESTED — Fresh challenge:** The selected final sign-in did not demonstrate a new Authenticator push or fresh MFA challenge.

## Security controls and limitations
The policy targeted a dedicated test user rather than all users, reducing risk to the administrator account. Report-only testing preceded enforcement. The evidence establishes the observed Conditional Access outcomes for the selected sign-ins; it does not prove every application, device, network, or future sign-in will behave identically. The final event used an existing authentication claim. No production deployment, enterprise approval, phishing-resistance assessment, or break-glass recovery exercise was performed.

## Evidence
See [screenshot inventory](../screenshots/README.md). Evidence filenames are the intended manual uploads and should be linked only after the actual images are committed.

## Analyst takeaways
A successful sign-in is not sufficient evidence of how an MFA requirement was fulfilled. Review the policy result **and** Authentication Details; distinguish a report-only prediction, an enforced-policy result, and the method used to satisfy MFA.
