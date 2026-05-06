# Standards & API Reference

> Project: Payment Processing Platform · Generated: 2026-05-03

## Industry Standards & Specifications

### ISO Standards

**ISO 8583 — Financial Transaction Card-Originated Messages**
- URL: https://www.iso.org/standard/79451.html
- The foundational card-payment message format used by Visa, Mastercard, and acquirers worldwide since the 1980s. Defines message type indicators (MTIs), up to 192 data elements, and code values for purchase, withdrawal, reversal, authorisation, and reconciliation flows. The 2023 edition (ISO 8583:2023) is the current revision. Any platform that connects directly to card networks or legacy acquirers must support or translate to/from ISO 8583.

**ISO 20022 — Financial Services — Universal Financial Industry Message Scheme**
- URL: https://www.swift.com/standards/iso-20022 and https://www.iso.org/standard/66946.html
- The modern, XML/JSON-based replacement for ISO 8583 and legacy MT message formats. Adopted by SWIFT for cross-border payments (coexistence period with MT ended November 2025), Fedwire, TARGET2, and SEPA. Carries richer structured data (remittance information, legal entity identifiers) enabling straight-through processing and fraud analytics. Any platform targeting international bank transfers or connecting to modern payment rails must support ISO 20022 message sets (pacs, pain, camt).

**ISO 27001 — Information Security Management Systems**
- URL: https://www.iso.org/standard/27001
- Widely referenced security management standard. While not payment-specific, PCI DSS assessors and enterprise buyers routinely require ISO 27001 certification as evidence of systematic security governance alongside PCI compliance.

**ISO 4217 — Currency Codes**
- URL: https://www.iso.org/iso-4217-currency-codes.html
- The authoritative list of three-letter alphabetic currency codes (USD, EUR, GBP, etc.) and their numeric equivalents. All payment amount fields and multi-currency logic must reference ISO 4217 codes.

### Payment Card Industry Standards (PCI SSC)

**PCI DSS 4.0.1 — Payment Card Industry Data Security Standard**
- URL: https://www.pcisecuritystandards.org/standards/
- The mandatory compliance framework for any entity that stores, processes, or transmits cardholder data. Version 4.0.1 became fully enforced as of March 31, 2025. Key v4.0 additions include mandatory MFA for all cardholder data environment (CDE) access, web-script inventory and justification requirements to prevent Magecart-style attacks, and an outcomes-based customised approach for controls. Non-compliance fines range from $5,000–$100,000/month. A payment platform must achieve and maintain SAQ-A, SAQ-D, or QSA-assessed compliance depending on its integration architecture.

**EMV Chip Specifications**
- URL: https://www.emvco.com/emv-technologies/contact/
- The Europay–Mastercard–Visa chip card standard mandating cryptographic transaction authentication for card-present payments. Liability shift (2015 in the US) means merchants not accepting EMV bear chargeback liability for counterfeit fraud. Relevant for any platform supporting point-of-sale terminals.

**EMV 3-D Secure (3DS2) v2.3.1**
- URL: https://www.emvco.com/emv-technologies/3-d-secure/
- The current e-commerce authentication standard for card-not-present transactions. Transmits 40+ required and up to 150 optional data elements to the card issuer for risk-based authentication, enabling frictionless approvals for low-risk transactions. Version 2.3.1 adds WebAuthn/SPC integration for passkey-based authentication. Mandated for Strong Customer Authentication (SCA) under PSD2. A payment platform must integrate 3DS2 flows for EU-facing merchants.

**EMV Payment Tokenisation**
- URL: https://www.emvco.com/emv-technologies/payment-tokenisation/
- Specifies how primary account numbers (PANs) are replaced with network tokens for digital wallets (Apple Pay, Google Pay, Samsung Pay) and card-on-file transactions. Reduces PCI scope and fraud exposure. Platforms supporting recurring billing or digital wallets must implement EMV tokenisation.

### W3C & IETF Standards

**W3C Payment Request API (Candidate Recommendation)**
- URL: https://www.w3.org/TR/payment-request/
- Browser-native API enabling merchants to invoke the browser's built-in payment sheet, surfacing saved cards, Apple Pay, Google Pay, and other payment handlers without a redirect. Updated January 2026 (CRD status). Reduces checkout friction and PCI scope for web integrations.

**W3C Payment Handler API**
- URL: https://www.w3.org/TR/payment-handler/
- Companion to the Payment Request API; allows web apps (e.g. bank apps, wallet apps) to register as payment handlers in the browser. Enables open-banking account-to-account payments directly in the checkout flow.

**W3C Secure Payment Confirmation (SPC)**
- URL: https://www.w3.org/TR/secure-payment-confirmation/
- Combines WebAuthn/FIDO2 with transaction-specific data (amount, merchant, payee) displayed in a browser-native dialog to satisfy PSD2 dynamic linking requirements. Integrated with EMV 3DS 2.3. Provides phishing-resistant SCA with minimal user friction.

**RFC 7807 — Problem Details for HTTP APIs**
- URL: https://www.rfc-editor.org/rfc/rfc7807
- Standardises error response bodies for HTTP APIs (application/problem+json). Payment APIs return diverse error conditions (insufficient funds, card declined, velocity exceeded); adopting RFC 7807 makes error handling predictable for integrators.

**RFC 6749 / RFC 6750 — OAuth 2.0 Authorization Framework**
- URL: https://www.rfc-editor.org/rfc/rfc6749
- The foundational authorisation framework used by open-banking APIs, merchant onboarding flows, and third-party integrations. Required for PSD2-compliant access to bank account data and payment initiation.

**RFC 7519 — JSON Web Tokens (JWT)**
- URL: https://www.rfc-editor.org/rfc/rfc7519
- Token format used for API bearer tokens, webhook signatures, and inter-service authentication. Used extensively by Stripe, Adyen, and modern payment gateways for stateless session management.

### Data Model & API Specifications

**OpenAPI Specification 3.1 / 3.2**
- URL: https://spec.openapis.org/oas/v3.1.0.html and https://spec.openapis.org/oas/v3.2.0.html
- The de-facto standard for documenting REST payment APIs. All major payment platforms (Stripe, Adyen, Checkout.com, PayPal) publish OpenAPI specs. Building to OAS 3.1+ enables automated SDK generation, interactive documentation, and contract testing. Note: monetary amounts must use type `string` or `integer` (minor currency units) rather than `float` to avoid precision loss.

**JSON Schema (Draft 2020-12)**
- URL: https://json-schema.org/
- Used within OpenAPI specs to define payment object schemas (PaymentIntent, Charge, Refund, Webhook event). Enables runtime validation and auto-generated type definitions.

**ISO 4217 numeric amounts convention**
- Best practice (followed by Stripe and Adyen) of expressing monetary amounts as integers in the smallest currency unit (e.g. cents for USD, pence for GBP) to prevent floating-point rounding errors in payment calculations.

### Regulatory Frameworks

**PSD2 — EU Payment Services Directive 2 (2015/2366/EU)**
- URL: https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32015L2366
- The EU regulatory framework requiring Strong Customer Authentication (SCA) for electronic payments, mandating open-banking API access to bank accounts, and defining the roles of Account Servicing Payment Service Providers (ASPSPs), Payment Initiation Service Providers (PISPs), and Account Information Service Providers (AISPs). Any platform serving EU merchants or customers must align with PSD2's SCA and data-sharing requirements.

**NACHA Operating Rules (ACH Network)**
- URL: https://www.nacha.org/
- Governance framework for the US Automated Clearing House (ACH) network, administered by Nacha (est. 1974). Covers authorisation requirements, return codes, data security (encryption, access controls), and same-day ACH. 2026 rule changes require risk-based fraud detection for outbound ACH entries and will raise the Same Day ACH per-entry limit to $10 million (effective September 2027). Mandatory for platforms originating ACH debits or credits in the US.

**SEPA Credit Transfer / Instant (SCT / SCT Inst) — EPC Rulebooks**
- URL: https://www.europeanpaymentscouncil.eu/what-we-do/epc-payment-schemes/sepa-credit-transfer
- The European Payments Council's rulebooks governing euro bank transfers across 36 SEPA countries. The 2025 v1.0 SCT Inst implementation guidelines are based on the 2019 ISO 20022 message version and entered into force October 2025 under the EU Instant Payments Regulation (EU 2024/886). Platforms targeting European bank-transfer payments must implement the EPC/ISO 20022 message formats.

**GDPR — General Data Protection Regulation (EU 2016/679)**
- URL: https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32016R0679
- Governs collection, storage, and processing of EU personal data. Creates a tension with AML/KYC data-retention obligations (which require retaining customer identity records for 5–10 years). Payment platforms must implement data-minimisation, purpose-limitation, and secure deletion controls. Fines reach 4% of global annual turnover.

**AML / KYC — 6th EU Anti-Money Laundering Directive (AMLD6) and US BSA/FinCEN**
- URL: https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32018L1673 and https://www.fincen.gov/
- Requires identity verification (KYC) of customers before processing payments above thresholds, ongoing transaction monitoring for suspicious activity, and reporting to financial intelligence units. Platforms operating as money-service businesses or payment institutions must build or integrate KYC/AML screening (sanctions lists, PEP screening, transaction monitoring).

### Security & Authentication Standards

**Financial-grade API (FAPI) 2.0 — OpenID Foundation**
- URL: https://fapi.openid.net/
- An OpenID Connect profile adding baseline and advanced security constraints (PAR, DPoP, JARM, mTLS) specifically for high-value financial API access. Adopted by open-banking frameworks in the UK (OBIE), EU (Berlin Group), Brazil, and Australia. Platforms exposing payment initiation or account-data APIs should target FAPI 2.0 Security Profile compliance.

**FIDO2 / WebAuthn — FIDO Alliance & W3C**
- URL: https://fidoalliance.org/fido2/ and https://www.w3.org/TR/webauthn/
- Public-key cryptographic authentication standard enabling phishing-resistant, device-bound user authentication using biometrics or hardware keys. Satisfies the "possession" and "inherence" factors of PSD2 SCA. Integrated with Secure Payment Confirmation (SPC) and EMV 3DS 2.3. Payment platforms implementing strong authentication for merchant portals or consumer checkout should support FIDO2.

**Berlin Group NextGenPSD2 Framework**
- URL: https://www.berlin-group.org/psd2-access-to-bank-accounts
- The dominant open-banking API standard in Europe; implemented by 75%+ of EU banks. Defines XS2A (Access to Account) API endpoints for payment initiation (PISP), account information (AISP), and confirmation of funds (CBPII) using OAuth2/FAPI security. Published under Creative Commons with OpenAPI 3 specifications available. A payment platform adding bank-transfer payment initiation in Europe must support or translate the NextGenPSD2 interface.

**OWASP API Security Top 10 (2023)**
- URL: https://owasp.org/API-Security/editions/2023/en/0x00-header/
- The authoritative checklist of API security risks (broken object-level authorisation, authentication failures, excessive data exposure, etc.). Payment APIs handling sensitive cardholder and bank data are high-value attack targets; a payment platform should be designed and audited against the OWASP API Security Top 10.

---

## Similar Products — Developer Documentation & APIs

### Stripe

- **Description:** Full-stack payment platform with APIs for accepting payments, subscriptions, payouts, fraud (Radar), and financial services. Widely regarded as the gold standard for developer experience.
- **API Documentation:** https://docs.stripe.com/api
- **SDKs/Libraries:** Official libraries for Node.js, Python, Ruby, PHP, Java, Go, .NET; mobile SDKs for iOS and Android — https://docs.stripe.com/libraries
- **Developer Guide:** https://docs.stripe.com/development
- **Webhook Documentation:** https://docs.stripe.com/webhooks
- **Standards:** REST/JSON; OpenAPI spec available; v2 API namespace launched 2024; amounts expressed as integers in minor currency units
- **Authentication:** API Key (Bearer token in Authorization header); restricted keys for least-privilege access; webhook signature verification via HMAC-SHA256

### Adyen

- **Description:** Enterprise payment platform with global acquiring, interchange-plus pricing, and a unified commerce (online + in-person) API.
- **API Documentation:** https://docs.adyen.com/ and API Explorer at https://docs.adyen.com/api-explorer/
- **SDKs/Libraries:** Server-side SDKs for Java, .NET, PHP, Python, Node.js, Go, Ruby — https://docs.adyen.com/development-resources/libraries/
- **Developer Guide:** https://developers.adyen.com/
- **Standards:** REST/JSON; OpenAPI/Swagger specs available; Terminal API (JSON-over-NEXO) for POS
- **Authentication:** API Key (x-API-key header); Basic Auth (legacy); HMAC webhook signatures; mTLS for advanced setups

### PayPal / Braintree

- **Description:** PayPal provides consumer-facing and merchant payment APIs. Braintree (owned by PayPal) is the developer-first gateway with transparent pricing and a GraphQL API.
- **API Documentation (PayPal REST):** https://developer.paypal.com/api/rest/
- **API Documentation (Braintree):** https://developer.paypal.com/braintree/docs/
- **Braintree GraphQL:** https://developer.paypal.com/braintree/graphql/guides/concepts/
- **SDKs/Libraries:** Java, PHP, Python, Node.js, Ruby, .NET for PayPal; same plus iOS/Android for Braintree
- **Standards:** REST/JSON (PayPal v2); GraphQL (Braintree); OpenAPI specs available; PayPal v1/payments endpoints are being deprecated in favour of v2/checkout/orders
- **Authentication:** OAuth 2.0 client-credentials for PayPal REST; API key + client token for Braintree

### Square

- **Description:** Integrated payments and commerce platform targeting SMBs, restaurants, and retail. REST APIs for payments, orders, invoices, subscriptions, and in-person terminals.
- **API Documentation:** https://developer.squareup.com/docs
- **API Reference:** https://developer.squareup.com/reference/square
- **SDKs/Libraries:** Python, Node.js, Ruby, PHP, Java, .NET, Go — https://developer.squareup.com/docs/sdks
- **Developer Guide:** https://developer.squareup.com/docs/payments-overview
- **Standards:** REST/JSON; OpenAPI spec published; Node.js and Python SDKs fully rewritten in 2025 to support Lambda, Cloudflare Workers, etc.; idempotency keys on all mutating calls
- **Authentication:** OAuth 2.0 (for third-party apps); Access Token in Authorization header (for own-account integrations)

### Checkout.com

- **Description:** Enterprise payment platform with 150+ processing currencies, advanced ML fraud tools, and strong international acquiring in markets where Stripe has limited reach.
- **API Documentation:** https://www.checkout.com/docs and https://api-reference.checkout.com/
- **Developer Guide:** https://www.checkout.com/docs/developer-resources/api
- **Standards:** REST/JSON; OpenAPI spec available; Unified Payments API covers cards, APMs, and digital wallets through a single endpoint
- **Authentication:** API key pairs (public/secret); HMAC webhook signatures; OAuth 2.0 for platform/marketplace sub-entity access

### Dwolla (ACH specialist)

- **Description:** US ACH and real-time payment API platform for bank-to-bank transfers, payroll, marketplace payouts, and account verification. Integrates with Plaid for instant bank account verification.
- **API Documentation:** https://developers.dwolla.com/
- **Integration Guide (Plaid + Dwolla):** https://developers.dwolla.com/guides/plaid/create-funding-source
- **SDKs/Libraries:** PHP, Ruby, Python, Node.js, Java, C#
- **Standards:** REST/JSON; HAL hypermedia links; supports ACH (standard and same-day), RTP (Real-Time Payments), and Wire
- **Authentication:** OAuth 2.0 (client credentials); webhook HMAC-SHA256 signatures

### Mollie

- **Description:** European payment service provider with a clean REST API supporting cards, iDEAL, SEPA, Klarna, and 30+ local payment methods. Popular in the Netherlands, Belgium, and Germany.
- **API Documentation:** https://docs.mollie.com/
- **Developer Portal:** https://www.mollie.com/developers
- **SDKs/Libraries:** PHP, Ruby, Node.js, Python; plus community-maintained libraries for Go, Java, .NET
- **Standards:** REST/JSON; HAL+JSON hypermedia; OpenAPI spec available
- **Authentication:** API Key in Authorization header; OAuth 2.0 for platform/partner access

### Razorpay

- **Description:** Leading Indian payment gateway supporting 100+ payment methods including UPI, cards, net banking, and wallets. REST API with broad SDK coverage.
- **API Documentation:** https://razorpay.com/docs/api/
- **Developer Hub:** https://razorpay.com/docs/
- **SDKs/Libraries:** Node.js, Python, Ruby, PHP, Java, Go, .NET; Android and iOS SDKs
- **Standards:** REST/JSON; base URL https://api.razorpay.com/v1; webhook HMAC-SHA256 signature verification
- **Authentication:** API Key ID + Secret (Basic Auth); webhook signature validation

### Adyen Terminal API (POS)

- **Description:** In-person payment integration standard for connecting software to Adyen-certified terminals. Uses JSON over NEXO protocol.
- **API Documentation:** https://docs.adyen.com/point-of-sale/design-your-integration/terminal-api
- **Standards:** NEXO Retailer Protocol (ISO 23550-based); JSON encoding; cloud-based and local communication modes
- **Authentication:** API key + terminal ID; HMAC message-level security for local mode

---

## Notes

**Emerging & Evolving Areas**

- **Real-Time Payments (RTP / FedNow):** The US Federal Reserve's FedNow instant payment service (launched 2023) and The Clearing House's RTP network are growing rapidly but lack a single developer API standard. Each bank exposes its own interface; aggregators like Dwolla and Moov abstract the differences.
- **A2A / Open Banking Payments:** PSD2-mandated APIs are mature in Europe (NextGenPSD2, UK Open Banking), but the US Financial Data Exchange (FDX) API standard for account-to-account payment initiation is still evolving with no legislative mandate.
- **Stablecoin / Digital Currency Payments:** CBDC pilots (Digital Euro, Digital Dollar) and stablecoin payment rails (USDC, USDT) are emerging but have no ratified ISO or W3C standards as of 2026. This is an area where regulatory guidance lags technical capability significantly.
- **MCP (Model Context Protocol) for Payment Agents:** No MCP server specification exists yet for payment processing. An AI-native platform could define a canonical MCP server that exposes payment operations (create payment, refund, dispute lookup) as structured tools for LLM agents — an area with no incumbent standard.
- **Currency precision:** The ISO 4217 standard does not specify minor-unit encoding for all currencies (e.g. JPY has zero decimal places; KWD has three). Payment platforms must maintain a currency metadata table to handle amounts correctly, as OpenAPI alone does not enforce this.
