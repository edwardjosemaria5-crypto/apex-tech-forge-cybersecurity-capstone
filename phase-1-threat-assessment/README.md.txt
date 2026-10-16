# Phase 1 — Threat Assessment and Security Policy

## Project

**APEX Tech Forge Academy Cybersecurity Capstone**

## Objective

Assess the Academy's primary cybersecurity risks and recommend practical controls to protect student records, staff information, and critical systems.

## Scenario

The Academy has experienced an increase in phishing attempts and unauthorised network scanning. This phase identifies priority threats and establishes an initial defensive action plan.

## Security Framework: CIA Triad

- **Confidentiality:** Restrict access to student records using strong authentication, least-privilege permissions, and encrypted communications.
- **Integrity:** Use cryptographic hashes, access controls, and audit logs to help detect unauthorised changes to records.
- **Availability:** Maintain protected backups, apply security updates, and test recovery procedures.

## Threat Assessment

| Threat                                         | Potential Impact                               | Recommended Mitigation                                                 |
| ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------------------------------- |
| Phishing                                       | Stolen credentials and unauthorised access     | Email filtering, security awareness training, and MFA                  |
| Ransomware                                     | Encrypted files and service disruption         | Protected backups, recovery testing, patching, and endpoint protection |
| Unauthorised network scanning and exploitation | Discovery and exploitation of exposed services | Firewall restrictions, disabling unnecessary services, and monitoring  |

## Recommended Defensive Controls

1. Configure encrypted SSH remote administration.
2. Restrict network traffic with firewall rules.
3. Protect sensitive files using appropriate permissions.
4. Verify file integrity using SHA-256 hashes.
5. Monitor network traffic and authentication logs.

## Current Status

- [x] Executive summary drafted.
- [x] CIA Triad applied to the Academy's scenario.
- [x] Three priority threats and mitigations identified.
- [ ] Practical controls implemented and verified in later phases.

## Reflection

This phase established a risk-based approach to protecting the Academy. The next phases will test technical controls in a controlled lab environment and document the results.

## Scope and Safety

Testing will be performed only on systems owned by the student or explicitly authorised for the exercise. Screenshots and findings will be reviewed for sensitive information before publication.
