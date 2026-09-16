# Healthcare Web Application Security Assessment

> Sanitized portfolio version — all client identifiers, production URLs, credentials, tokens, personal data, internal hostnames, and directly reusable exploitation details have been removed.

## Overview

This project documents an authorized penetration testing engagement against a healthcare information system. The assessment focused on authenticated web-application and API security, with particular attention to broken access control, privilege escalation, excessive data exposure, insecure credential handling, and production diagnostic exposure.

The original engagement report was confidential. This repository contains only a portfolio-safe summary of the work and methodology. It must not be used to infer, target, or test any real production system.

## Scope

The assessment covered a representative healthcare web application and its REST API. Testing included:

- Authentication and authorization checks across multiple user roles.
- Role and permission management controls.
- User, employee, and account-management endpoints.
- Exposure of administrative metadata and sensitive fields.
- Client-side bundles and configuration handling.
- Production diagnostic and profiling exposure.
- Negative authorization testing for actions that should be restricted.

No patient records, real credentials, access tokens, or personal information are included in this repository.

## Key Findings Summary

The assessment identified critical authorization and secret-management weaknesses in the assessed environment:

1. A low-privileged authenticated role could modify role permissions without an appropriate administrative authorization check.
2. Administrative user, role, and permission data was accessible beyond the intended business need.
3. Production diagnostic information disclosed internal application metadata.
4. A default administrative credential was embedded in a publicly served client-side bundle.
5. An attacker who gained elevated permissions could create a persistent privileged account through employee-management functionality.

The findings demonstrated that authentication alone was being relied upon in places where server-side, operation-specific authorization was required.

## Methodology

Testing was performed manually using an intercepting proxy and controlled test accounts. The assessment followed principles from:

- OWASP Web Security Testing Guide.
- OWASP Top 10.
- OWASP API Security Top 10.
- Penetration Testing Execution Standard.
- CVSS v3.1 risk-rating guidance.

Automated tools were used only where appropriate for supporting checks. Confirmed findings were validated through controlled request and response analysis rather than scanner output alone.

## Recommended Remediation Themes

- Enforce server-side authorization for every privileged read and write operation.
- Apply object-level and field-level authorization to administrative resources.
- Remove credentials, tokens, and secrets from frontend source code and compiled assets.
- Rotate exposed credentials and invalidate related sessions and tokens.
- Disable production profiling endpoints or restrict them to authorized administrators.
- Add audit logging and alerting for permission changes, role assignment, employee creation, and account creation.
- Add automated negative authorization tests that assert `401` or `403` responses for unauthorized roles.
- Retest the affected controls with fresh accounts and newly issued tokens after remediation.

## Portfolio Disclaimer

This repository is a sanitized professional portfolio artifact. It does not contain the original confidential report, real target identifiers, production API paths, credentials, tokens, screenshots, request captures, patient information, employee information, or exploit-ready evidence.

Only publish this repository after confirming that the client has authorized public disclosure of the high-level project description.

## Repository Contents

- [`sanitized-assessment-summary.md`](sanitized-assessment-summary.md): portfolio-safe technical summary.
- [`SECURITY.md`](SECURITY.md): disclosure and handling guidance.
- [`linkedin-post.md`](linkedin-post.md): suggested LinkedIn post.
- [`cv-project-entry.md`](cv-project-entry.md): CV project descriptions.
- [`.gitignore`](.gitignore): baseline exclusion rules for secrets and local files.
