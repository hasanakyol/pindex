# Security Checklist - Modern Security Threats (2025)

This checklist addresses current security vulnerabilities including OWASP Top 10, AI/LLM risks, and supply chain attacks relevant for 2025.

## 🔒 Critical Security Threats (2025)

### 1. Broken Access Control & Zero Trust
- [ ] Implement proper authentication before allowing access to resources
- [ ] Use role-based access control (RBAC) or attribute-based access control (ABAC)
- [ ] Deny by default - explicitly grant permissions
- [ ] Disable directory listing and ensure no backup files are accessible
- [ ] Rate limit API calls to prevent abuse
- [ ] Log access control failures and alert on repeated failures
- [ ] Invalidate JWT tokens on logout (use a blacklist or short expiry)

### 2. Supply Chain & Dependency Attacks
- [ ] Use Socket.dev or Snyk for real-time supply chain monitoring
- [ ] Implement SBOM (Software Bill of Materials) generation
- [ ] Pin all dependencies with lock files (bun.lockb, package-lock.json)
- [ ] Use private npm registries for internal packages
- [ ] Verify package signatures and checksums
- [ ] Monitor for typosquatting and dependency confusion attacks
- [ ] Implement automated dependency updates with security scanning
- [ ] Use npm audit signatures and provenance

### 3. AI/LLM Prompt Injection & Data Poisoning
- [ ] Sanitize all inputs before sending to AI/LLM APIs
- [ ] Implement prompt validation and filtering
- [ ] Use structured outputs with JSON schema validation
- [ ] Rate limit AI API calls per user
- [ ] Monitor for prompt injection patterns
- [ ] Implement content moderation for AI responses
- [ ] Separate system prompts from user inputs
- [ ] Use prompt templates with strict boundaries
- [ ] Log and audit all AI interactions

### 4. API Security & GraphQL Vulnerabilities
- [ ] Implement API rate limiting with Redis or Upstash
- [ ] Use API versioning and deprecation policies
- [ ] Validate GraphQL query depth and complexity
- [ ] Implement field-level authorization in GraphQL
- [ ] Use API gateways (Kong, Tyk, AWS API Gateway)
- [ ] Implement request/response schema validation
- [ ] Monitor API abuse patterns
- [ ] Use OAuth 2.1 or JWT with short expiry
- [ ] Implement API key rotation

### 5. Cloud & Container Security
- [ ] Scan container images with Trivy or Snyk
- [ ] Use distroless or minimal base images
- [ ] Implement Pod Security Standards in Kubernetes
- [ ] Use AWS IMDSv2, Azure Managed Identity
- [ ] Enable cloud provider security services (GuardDuty, Security Center)
- [ ] Implement proper S3/blob storage policies
- [ ] Use Secrets Manager (AWS, Azure, HashiCorp Vault)
- [ ] Enable VPC endpoints and private subnets
- [ ] Implement cloud WAF and DDoS protection

### 6. Cryptographic Failures & Quantum Threats
- [ ] Use TLS 1.3 exclusively (disable older versions)
- [ ] Implement post-quantum cryptography readiness
- [ ] Use Argon2id for password hashing (bcrypt is outdated)
- [ ] Implement encryption key rotation (AWS KMS, Azure Key Vault)
- [ ] Use authenticated encryption (AES-256-GCM)
- [ ] Implement certificate pinning for mobile apps
- [ ] Use Hardware Security Modules (HSM) for critical keys
- [ ] Prepare for quantum-resistant algorithms (CRYSTALS-Kyber)

### 7. Modern Authentication & Identity Threats
- [ ] Implement passwordless authentication (WebAuthn, Passkeys)
- [ ] Use modern auth providers (Better-Auth, Clerk, Auth0, Supabase Auth)
- [ ] Implement risk-based authentication
- [ ] Use device fingerprinting and anomaly detection
- [ ] Implement FIDO2/WebAuthn standards
- [ ] Use Argon2id with appropriate cost factors
- [ ] Implement account takeover protection
- [ ] Use magic links over password resets
- [ ] Monitor for credential stuffing attacks

### 8. CI/CD & Software Supply Chain Security
- [ ] Use SLSA framework for supply chain security
- [ ] Implement signed commits and artifact signing
- [ ] Use GitHub Advanced Security or GitLab Security
- [ ] Implement SAST/DAST in CI pipeline
- [ ] Use Sigstore for artifact signing
- [ ] Implement build provenance and attestation
- [ ] Use ephemeral build environments
- [ ] Implement dependency review actions
- [ ] Use OpenSSF Scorecards

### 9. Observability & Threat Detection
- [ ] Implement OpenTelemetry for distributed tracing
- [ ] Use SIEM solutions (Datadog, Splunk, Elastic)
- [ ] Implement real-time threat detection
- [ ] Use structured logging with correlation IDs
- [ ] Implement audit logging for compliance
- [ ] Monitor for OWASP attack patterns
- [ ] Use AI-powered anomaly detection
- [ ] Implement incident response automation
- [ ] Use threat intelligence feeds

### 10. SSRF, CSRF & Modern Web Vulnerabilities
- [ ] Validate and sanitize all URLs
- [ ] Use allowlists for URL schemes, ports, and destinations
- [ ] Disable HTTP redirections
- [ ] Don't send raw responses to clients
- [ ] Use network segmentation
- [ ] Block requests to private IP ranges (10.x, 172.x, 192.168.x, 169.254.x)
- [ ] Monitor for DNS rebinding attacks

## 🛡️ 2025 Emerging Threats

### AI/LLM Security
- [ ] Implement LLM output validation and sanitization
- [ ] Monitor for hallucination and misinformation
- [ ] Implement cost controls for AI API usage
- [ ] Use prompt guards and content filters
- [ ] Implement PII detection in prompts
- [ ] Monitor for model extraction attempts
- [ ] Use local LLMs for sensitive data
- [ ] Implement AI red teaming

### Edge & Browser Security
- [ ] Implement CSP Level 3 with nonces
- [ ] Use Trusted Types API
- [ ] Implement Speculation Rules API securely
- [ ] Use Cross-Origin-Opener-Policy headers
- [ ] Implement Permission Policy
- [ ] Use Web Crypto API for client-side encryption
- [ ] Implement CORS-RFC1918 for private network access
- [ ] Monitor for Spectre-style attacks

### Zero Trust & Modern Infrastructure
- [ ] Implement Zero Trust Network Architecture
- [ ] Use service mesh (Istio, Linkerd) for mTLS
- [ ] Implement eBPF-based security monitoring
- [ ] Use Policy as Code (OPA, Kyverno)
- [ ] Implement GitOps with security scanning
- [ ] Use CNAPP platforms for cloud security
- [ ] Implement microsegmentation
- [ ] Use CASB for SaaS security

## 📋 Security Review Checklist

Before each deployment:
- [ ] Run automated security scans
- [ ] Review dependency vulnerabilities
- [ ] Check for exposed secrets
- [ ] Verify security headers
- [ ] Test authentication flows
- [ ] Review access controls
- [ ] Check error handling
- [ ] Verify logging is working
- [ ] Test rate limiting
- [ ] Validate input sanitization

## 🔧 Recommended Security Tools

### Static Analysis
- **Semgrep**: Custom security rules
- **CodeQL**: GitHub's code analysis
- **SonarQube**: Code quality and security
- **Snyk**: Vulnerability scanning

### Dynamic Analysis
- **OWASP ZAP**: Web app security scanner
- **Burp Suite**: Security testing platform
- **Nuclei**: Vulnerability scanner

### Dependency Scanning
- **Socket.dev**: Supply chain security
- **Snyk**: Vulnerability database
- **npm audit**: Built-in npm security
- **Dependabot**: Automated updates

### Runtime Protection
- **Sentry**: Error tracking with security insights
- **Datadog**: Security monitoring
- **Cloudflare**: WAF and DDoS protection
- **AWS WAF**: Web application firewall

## 📚 Resources

- [OWASP Top 10](https://owasp.org/Top10/)
- [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- [SLSA Supply Chain Security](https://slsa.dev/)
- [OpenSSF Best Practices](https://bestpractices.coreinfrastructure.org/)
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/)
- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)
- [CWE Top 25](https://cwe.mitre.org/top25/)

---
