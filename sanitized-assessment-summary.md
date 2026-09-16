# Sanitized Security Assessment Summary

## Engagement Context

An authorized authenticated penetration test was performed against a healthcare information system. The objective was to evaluate whether role boundaries, administrative APIs, credential handling, and production diagnostics enforced least privilege and protected sensitive operations.

This public summary intentionally omits the client name, production host, exact endpoint paths, account identifiers, credentials, tokens, personal data, internal hostnames, screenshots, and raw request or response evidence.

## Assessment Approach

The work combined passive technology review with manual authenticated testing. Controlled test accounts representing a low-privileged operational role and an administrative role were used to compare authorization behavior. Requests were inspected and replayed through an intercepting proxy, and each material issue was validated using a reproducible request and response pattern in the authorized environment.

The assessment used OWASP Web Security Testing Guide techniques, OWASP Top 10 and API Security Top 10 classifications, PTES engagement structure, CWE mappings, and CVSS v3.1 severity scoring.

## Principal Security Observations

### Broken Function-Level Authorization

A low-privileged authenticated user was able to invoke a role-permission management operation without the dedicated administrative authorization that should have protected it. This created a privilege-escalation path because the authorization model itself could be modified by an insufficiently trusted role.

### Excessive Administrative Data Exposure

Administrative collections exposed more user, role, permission, and account metadata than the tested role required for its business workflow. The issue increased the risk of identity enumeration, targeted phishing, and authorization-model discovery.

### Production Diagnostic Exposure

A diagnostic/profiling feature was reachable in the production deployment and disclosed internal application metadata. Production diagnostics should be disabled or restricted to a controlled administrative channel.

### Hardcoded Administrative Credential

A default administrative credential was present in a publicly downloadable client-side asset. Any value compiled into frontend JavaScript must be treated as public and cannot be used as a secret.

### Privileged Account Creation Through Inadequately Protected Workflow

After authorization was compromised, employee and account-management operations allowed creation of a new privileged account without an independent, narrowly scoped administrative check. This demonstrated the importance of protecting each sensitive operation independently rather than relying on a previously calculated permission set.

## Remediation Priorities

The highest-priority actions were to rotate exposed credentials, invalidate related sessions, remove secrets from client-side assets, enforce server-side authorization on every privileged operation, restrict administrative data fields, disable or protect production diagnostics, and add audit logging for permission and account changes.

A complete remediation validation should use fresh test accounts and newly issued tokens. Unauthorized operations should consistently return an authorization failure, while documented administrative workflows should continue to work for approved administrators.

## Skills Demonstrated

The engagement involved web and API penetration testing, manual request replay, authorization analysis, privilege-escalation validation, secret exposure review, OWASP-based classification, CVSS risk analysis, evidence handling, remediation planning, and retest design.

## Disclosure Note

This document is a portfolio-safe abstraction of a confidential engagement. It is not a vulnerability disclosure, does not identify the assessed organization, and must not be used to test any real system without explicit written authorization.
