# Sanitized Technical Appendix

## Testing Model

The assessment used a controlled role-based test model. A low-privileged operational account and an administrative reference account were compared against the same business functions. The objective was to determine whether authorization decisions were enforced server-side for each operation, resource, and returned field.

No real credentials, production values, patient records, employee data, tokens, or target-specific request captures are included here.

## Authorization Test Matrix

| Control area | Low-privileged role | Administrative reference role | Expected result |
|---|---:|---:|---|
| Read own operational data | Allowed | Allowed | Business-required fields only |
| Read administrative user catalogue | Denied or narrowly scoped | Allowed | No unnecessary identity or role metadata |
| Read role definitions | Denied or narrowly scoped | Allowed | Server-side policy enforcement |
| Modify role permissions | Denied | Allowed only when explicitly authorized | `403 Forbidden` for unauthorized roles |
| Create employee record | Denied unless business-justified | Allowed | Independent authorization check |
| Create privileged account | Denied | Restricted to approved provisioning workflow | High-risk action requires elevated authorization |
| Access production diagnostics | Denied | Restricted administrative access only | No public diagnostic output |

## Validation Logic

For each sensitive operation, the test process verified the following sequence:

1. Establish a fresh session for the selected test role.
2. Invoke the operation using only the permissions documented for that role.
3. Record the HTTP status, response fields, and observable state change.
4. Repeat the check with the administrative reference role where an approved workflow existed.
5. Confirm that authorization was enforced by the server rather than inferred from client-side visibility.
6. Restore any test-controlled state immediately after validation.

The public version intentionally omits target-specific routes, identifiers, headers, payloads, and response bodies.

## Safe Command Examples

The following examples are intentionally generic and use a local placeholder host. They are documentation examples only and must not be directed at a real system without written authorization.

```bash
# Set a local lab target only
export LAB_BASE_URL="http://localhost:8080"

# Check that an unauthenticated request is rejected
curl --fail-with-body --silent --show-error \
  -i "$LAB_BASE_URL/api/example/admin-resource"

# Check that a deliberately invalid token is rejected
curl --fail-with-body --silent --show-error \
  -i -H "Authorization: Bearer INVALID_TEST_TOKEN" \
  "$LAB_BASE_URL/api/example/admin-resource"
```

These examples do not reproduce any finding from the confidential engagement and contain no production identifiers or credentials.

## Evidence Handling

Evidence was classified by whether a behavior was directly confirmed, observed as a design weakness, or excluded because it lacked complete reproducible support. Raw captures were retained separately for authorized stakeholders and are not part of this portfolio repository.

## Risk Assessment

Findings were mapped to relevant OWASP, CWE, and API Security categories. Severity was assessed using CVSS v3.1 while considering privilege requirements, attack complexity, confidentiality impact, integrity impact, availability impact, and the healthcare context.

## Remediation Verification

A remediation retest should use fresh accounts and newly issued sessions. The retest should verify that unauthorized operations fail consistently, approved administrative workflows remain functional, stale permissions do not survive token refresh, diagnostic output is not publicly accessible, and no credential-like values remain in client-side assets.

## Safety Boundary

This appendix is a portfolio-safe description of testing technique. It is not an exploit guide, vulnerability disclosure, or authorization to test any system.
