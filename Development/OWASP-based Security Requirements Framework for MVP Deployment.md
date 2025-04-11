# OWASP-based Security Requirements Framework for MVP Deployment

## Purpose

This document outlines essential security measures that **must** be implemented prior to launching any Minimum Viable Product (MVP). These requirements address critical vulnerabilities, safeguard user data, and maintain application stability regardless of technology stack. The checklist is aligned with the OWASP Top 10 Web Application Security Risks framework to ensure comprehensive protection against the most common and dangerous security threats. This policy requires systematic code inspection for all OWASP Top 10 vulnerabilities, recognising that security must be built into the application rather than relying solely on perimeter defences. Failure to comply with this policy may result in data breaches, service disruptions, or financial losses.

## Mandatory Security Requirements

### 1. Implement Rate Limiting (Helps mitigate A01:2021-Broken Access Control)

- Rate limiting **shall** be applied to all API endpoints to prevent abuse by automated systems or malicious actors
- Implementation should occur at the application or infrastructure level depending on your technology stack
- This measure protects against:
  - Database overload
  - Excessive resource usage
  - Cost spikes
  - Denial of service attacks
- OWASP relevance: Helps prevent resource exhaustion attacks and brute force attempts

### 2. Configure Access Control on Database Tables and Implement CSRF Protections (Addresses A01:2021-Broken Access Control)

- Appropriate access control mechanisms **must** be enabled on all database tables from the outset
- Policies **shall** be configured to restrict data access based on user identity
- Users should only be able to access their own data unless specifically authorised otherwise
- Implementation should be configured according to your database system's security features and product requirements
- Cross-Site Request Forgery (CSRF) protections **must** be implemented:
  - Anti-CSRF tokens for state-changing operations
  - Same-Site cookie attributes (preferably 'Strict' or 'Lax')
  - Custom headers for AJAX requests
  - Verification of request origin
- CSRF protections must not rely solely on WAF capabilities
- OWASP relevance: Directly addresses the most critical web application security risk by preventing unauthorised data access and cross-site request forgery attacks

### 3. Incorporate Anti-Automation Measures and Strong Authentication (Addresses A07:2021-Identification and Authentication Failures)

- Anti-automation measures (such as CAPTCHA) **shall** be added to all authentication-related forms
- This prevents automated systems from generating fake accounts or attempting unauthorised access
- Required implementation areas:
  - Account registration forms
  - Login pages
  - Password reset workflows
- Multi-factor authentication (MFA) **should** be implemented for:
  - Administrative access
  - Access to sensitive data or functions
  - User accounts when appropriate for the application risk profile
- Session management **must** be implemented securely:
  - Session timeouts for inactive users
  - Automatic session invalidation after logout
  - Session rotation after authentication state changes
  - Secure session storage mechanisms
- Choose appropriate solutions based on your security requirements and user experience considerations
- OWASP relevance: Mitigates credential stuffing, brute force, and automated attacks against authentication systems

### 4. Enable Web Application Firewall Protection (Complementary defense for multiple OWASP Top 10 risks)

- A Web Application Firewall (WAF) **must** be activated as a complementary defense layer
- WAFs provide an additional security control but **must not** be considered a replacement for secure code
- This should be configured to help detect and block common attack vectors including:
  - SQL injection (A03:2021-Injection)
  - Cross-site scripting (XSS) (A03:2021-Injection)
  - Cross-site request forgery (CSRF)
  - Server-Side Request Forgery (A10:2021-SSRF)
- Implementation can be at the hosting, CDN, or application level depending on your infrastructure
- OWASP relevance: Provides an additional layer of defense against multiple Top 10 vulnerabilities, but does not excuse the need for secure code

### 5. Secure Credentials and Secrets (Addresses A02:2021-Cryptographic Failures)

- Credentials and secrets **shall not** be exposed in client-side code under any circumstances
- Required practices:
  - Store all secrets in environment variables or secure credential stores
  - Use server-side processing for sensitive operations
  - Regularly audit code for accidental exposure of secrets
  - Implement secrets rotation policies
  - Ensure proper encryption for sensitive data at rest and in transit
  - Use strong, up-to-date cryptographic algorithms and protocols
- **Policy:** Assume any code running on the client is publicly accessible
- OWASP relevance: Prevents exposure of sensitive data through cryptographic failures

### 6. Validate All Inputs Server-Side (Addresses A03:2021-Injection)

- Server-side validation **must** be implemented for all user inputs, regardless of client-side validation
- Inputs requiring validation include:
  - User credentials
  - Form submissions
  - Uploaded files
  - API request payloads
  - URL parameters
- Implementation must include:
  - Parameterised queries for database operations
  - Input sanitisation
  - Output encoding appropriate to the context
  - Content-Type validation for uploaded files
- **Policy:** Each missing validation check represents a potential vulnerability
- OWASP relevance: Primary defence against injection attacks (SQL, NoSQL, command, LDAP)

### 7. Audit and Clean Dependencies (Addresses A06:2021-Vulnerable and Outdated Components)

- All software dependencies **shall** be audited before launch to minimise the attack surface
- Required actions:
  - Run appropriate security audit tools for your technology stack
  - Remove unused packages and libraries
  - Address known vulnerabilities in dependencies
  - Document exception handling for any accepted risks
  - Favour established, well-maintained dependencies
  - Implement a process for regular updates and patch management
- OWASP relevance: Directly addresses the risk of using components with known vulnerabilities

### 8. Implement Monitoring and Logging (Addresses A09:2021-Security Logging and Monitoring Failures)

- Monitoring and logging systems **must** be in place to detect and respond to issues
- Required capabilities:
  - Centralised log collection
  - Error tracking and alerting
  - Performance monitoring
  - Security event logging
  - Log protection against tampering
- Events to track:
  - Authentication failures
  - Unusual traffic patterns
  - Server errors and exceptions
  - Administrative actions
  - Access control failures
  - Input validation failures
- **Minimum requirement:** Basic logging system with timestamp and contextual information
- **Log content protection:** Logs **must not** contain:
  - Passwords or credentials
  - Authentication tokens
  - Sensitive personal information
  - Payment card data
  - Health information
  - Other regulated or sensitive data in plain text
- OWASP relevance: Enables detection, response, and forensic analysis of security incidents

### 9. Implement Secure Configuration (Addresses A05:2021-Security Misconfiguration)

- All application environments **must** be configured securely with:
  - Hardened server configurations following industry standards
  - **Removal of default accounts and passwords**
  - Changing of all default credentials in third-party systems
  - Disabling of unnecessary features, ports, and services
  - Up-to-date patches for operating systems and applications
  - Implementation of security headers (HSTS, CSP, X-Content-Type-Options, etc.)
  - Error handling that doesn't reveal sensitive information
- Cookie settings **must** be configured securely:
  - `HttpOnly` flag for session cookies
  - `Secure` flag for all cookies
  - Appropriate `SameSite` attribute
  - Limited cookie lifetime
  - Scoped paths and domains
- A security configuration review **shall** be conducted before launch
- OWASP relevance: Directly addresses misconfiguration vulnerabilities that often provide attackers with unauthorised access

### 10. Apply Security in Design and Development (Addresses A04:2021-Insecure Design)

- Security considerations **must** be integrated into the design phase with:
  - Threat modelling for high-risk functionality
  - Security requirements defined alongside functional requirements
  - Implementation of secure defaults
  - Principle of least privilege applied throughout
  - Defence in depth strategies
  - Secure failure modes
- Code must be systematically inspected for OWASP Top 10 vulnerabilities:
  - Structured code reviews by security-trained developers
  - Automated static application security testing (SAST)
  - Interactive application security testing (IAST) where appropriate
  - Penetration testing for critical functionality
  - Review of custom algorithms and security controls
- Each OWASP Top 10 category must be specifically addressed during code review:
  - A01: Broken Access Control – Verify proper authorisation checks
  - A02: Cryptographic Failures – Verify proper implementation of encryption
  - A03: Injection – Check for parameterised queries and input validation
  - A04: Insecure Design – Verify security requirements implementation
  - A05: Security Misconfiguration – Check for hardcoded settings
  - A06: Vulnerable Components – Verify proper component integration
  - A07: Identification and Authentication Failures – Check authentication flows
  - A08: Software and Data Integrity Failures – Verify integrity checks
  - A09: Logging and Monitoring Failures – Check logging implementation
  - A10: SSRF – Verify URL validation and network segmentation
- OWASP relevance: Addresses fundamental security flaws at the design and implementation level

### 11. Ensure Software and Data Integrity (Addresses A08:2021-Software and Data Integrity Failures)

- Measures **must** be implemented to protect against integrity violations:
  - Verification of software and data sources
  - Digital signatures for critical components
  - Secure build and deployment pipelines
  - Protection against unauthorized code modification
  - Validation of data from untrusted sources
  - Integrity checks for critical business data
- Third-party integrations **shall** be vetted for security compliance
- OWASP relevance: Prevents compromise through malicious updates or untrusted sources

### 12. Prevent Server-Side Request Forgery (Addresses A10:2021-SSRF)

- Protection against SSRF attacks **must** be implemented:
  - Sanitise and validate all client-supplied input data, especially URLs
  - Implement allowlists for external resource access
  - Disable HTTP redirections where possible
  - Enforce URL schemas, ports, and destinations with allowlists
  - Segregate remote resource access functionality in separate networks
  - Block access to localhost and private networks from public servers
- OWASP relevance: Directly addresses this sophisticated attack vector that can circumvent network protections

### 13. Conduct Comprehensive Code Review for OWASP Top 10 (Cross-cutting requirement)

- All application code **must** be systematically reviewed for OWASP Top 10 vulnerabilities prior to deployment:
  - Dedicated security code review sessions must be conducted
  - Code review checklists must specifically address each OWASP Top 10
  - Reviews must be performed by developers with security training
  - Results must be documented with remediation steps for any findings
- Automated tools **shall** be used to supplement manual review:
  - Static application security testing (SAST)
  - Software composition analysis (SCA)
  - Dynamic application security testing (DAST) where applicable
- A security sign-off process **must** be established with:
  - Clear acceptance criteria for each OWASP Top 10 category
  - Required approvals before deployment
  - Documentation of any accepted risks with mitigation strategies
- OWASP relevance: Cross-cutting requirement that validates protection against all Top 10 categories

### 14. Implement Secure Session Management (Addresses A07:2021-Identification and Authentication Failures)

- All session management mechanisms **must** be implemented securely:
  - Secure cookie configuration:
    - `HttpOnly` flag to prevent JavaScript access
    - `Secure` flag to ensure transmission over HTTPS only
    - `SameSite` attribute (preferably 'Strict' or 'Lax') to prevent CSRF
    - Appropriate domain and path restrictions
  - Session tokens must:
    - Be cryptographically strong and random
    - Be unique for each session
    - Have appropriate length and entropy
    - Be stored securely on the server
  - Session lifecycle controls must include:
    - Absolute session timeout (e.g., 24 hours)
    - Idle session timeout (e.g., 15-30 minutes of inactivity)
    - Immediate invalidation upon logout
    - Rotation after privilege level changes
  - Session revocation mechanisms must be implemented:
    - Ability to terminate all active sessions for a user
    - Administrative capability to revoke specific sessions
- OWASP relevance: Prevents session hijacking, fixation, and related authentication attacks

The following table maps each security requirement to the OWASP Top 10 (2021) risks it addresses:

| OWASP Risk                                           | Addressed by Requirement(s)                                    |
|------------------------------------------------------|----------------------------------------------------------------|
| A01:2021-Broken Access Control                       | 2. Configure Access Control on Database Tables and Implement CSRF Protections |
|                                                      | 1. Implement Rate Limiting (partial)                           |
|                                                      | 13. Conduct Comprehensive Code Review for OWASP Top 10         |
| A02:2021-Cryptographic Failures                      | 5. Secure Credentials and Secrets                              |
|                                                      | 13. Conduct Comprehensive Code Review for OWASP Top 10         |
| A03:2021-Injection                                   | 6. Validate All Inputs Server-Side                             |
|                                                      | 4. Enable Web Application Firewall Protection                  |
|                                                      | 13. Conduct Comprehensive Code Review for OWASP Top 10         |
| A04:2021-Insecure Design                            | 10. Apply Security in Design and Development                   |
|                                                      | 13. Conduct Comprehensive Code Review for OWASP Top 10         |
| A05:2021-Security Misconfiguration                   | 9. Implement Secure Configuration                              |
|                                                      | 13. Conduct Comprehensive Code Review for OWASP Top 10         |
| A06:2021-Vulnerable and Outdated Components          | 7. Audit and Clean Dependencies                                |
|                                                      | 13. Conduct Comprehensive Code Review for OWASP Top 10         |
| A07:2021-Identification and Authentication Failures  | 3. Incorporate Anti-Automation Measures and Strong Authentication |
|                                                      | 14. Implement Secure Session Management                        |
|                                                      | 13. Conduct Comprehensive Code Review for OWASP Top 10         |
| A08:2021-Software and Data Integrity Failures        | 11. Ensure Software and Data Integrity                         |
|                                                      | 13. Conduct Comprehensive Code Review for OWASP Top 10         |
| A09:2021-Security Logging and Monitoring Failures    | 8. Implement Monitoring and Logging                            |
|                                                      | 13. Conduct Comprehensive Code Review for OWASP Top 10         |
| A10:2021-Server-Side Request Forgery (SSRF)          | 12. Prevent Server-Side Request Forgery                        |
|                                                      | 4. Enable Web Application Firewall Protection (partial)        |
|                                                      | 13. Conduct Comprehensive Code Review for OWASP Top 10         |

## Compliance Statement

This security policy ensures that MVPs are launched with appropriate protections in place. Adherence to this checklist is mandatory to maintain user trust, ensure sustainable growth, and prevent security incidents. Development teams **shall** verify compliance with all requirements before each production deployment.

By following this OWASP Top 10 aligned checklist, organisations can significantly reduce the risk of security breaches and establish a foundation for secure application development. The policy emphasises that secure applications must be built from the ground up with proper code design and inspection, not just protected by external security controls.

## Document Control

| Version | Date       | Description                                                    |
|---------|------------|----------------------------------------------------------------|
| 1.0     | 11/04/2025 | Initial release                                                |
| 1.1     | 11/04/2025 | Updated to incorporate OWASP Top 10 (2021)                     |
| 1.2     | 11/04/2025 | Enhanced to require code inspection for OWASP Top 10 vulnerabilities |
| 1.3     | 11/04/2025 | Added explicit CSRF protections, secure session management, and other enhancements |