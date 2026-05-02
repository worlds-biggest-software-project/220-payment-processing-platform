# Payment Processing Platform

> Candidate #220 · Researched: 2026-05-02

## Existing Products and Software Packages

| Tool | Description | Type | Pricing | Strengths / Weaknesses |
|------|-------------|------|---------|------------------------|
| Stripe | Full-stack payment platform with gateway, fraud (Radar), reconciliation, and issuing | SaaS | 2.9% + $0.30 per card transaction (standard); custom interchange++ at scale | Best developer experience; broad product surface; pricing less competitive at very high volume |
| Adyen | Enterprise payment platform with interchange++ pricing and global acquiring | SaaS | Interchange++ custom (processing minimum required) | Preferred by large merchants (Spotify, Uber, eBay); requires engineering resources; not SMB-friendly |
| Braintree (PayPal) | Developer-first payment gateway with transparent interchange-plus pricing | SaaS | 2.59% + $0.45 per transaction standard; volume discounts to ~0.06% + $0.06 | Competitive volume pricing; PayPal ecosystem; declining developer mindshare vs. Stripe |
| Checkout.com | Payment platform for enterprise merchants with 150+ processing currencies | SaaS | Custom enterprise | Strong international acquiring; advanced ML fraud tools; less known in North America |
| Nuvei | Payments infrastructure covering 200+ markets, 150 currencies, 700+ payment methods | SaaS | Custom | Strong alternative payment method (APM) coverage; good for global expansion |
| Cybersource (Visa) | Payment management platform with Decision Manager fraud suite | SaaS | Custom | Visa network access; strong fraud tooling; legacy UI; enterprise-only |
| Square | Integrated payment and commerce platform for SMBs and restaurants | SaaS | 2.6% + $0.10 in-person; 2.9% + $0.30 online | Exceptional SMB and restaurant vertical; hardware ecosystem; limited enterprise depth |
| Authorize.net (Visa) | Payment gateway for card-present and card-not-present transactions | SaaS | $25/mo + 2.9% + $0.30 | Wide merchant integrations; mature and stable; dated technology compared to Stripe |
| Worldpay (FIS) | Global payment processing for enterprise merchants and financial institutions | SaaS | Custom enterprise | Massive global reach; acquired by FIS then spun out; complex commercial model |
| Airwallex | Multi-currency business payments, FX, and embedded finance infrastructure | SaaS | Custom / transaction-based | Strong FX and multi-currency; growing API-first platform; less name recognition than Stripe |

## Relevant Industry Standards or Protocols

- **PCI DSS (Payment Card Industry Data Security Standard)** — mandatory compliance framework for all entities storing, processing, or transmitting cardholder data
- **EMV (Europay, Mastercard, Visa)** — global standard for chip card transactions; liability shift drives hardware compliance requirements
- **ISO 20022** — next-generation financial messaging standard for payment instructions; adopted by SWIFT and Fedwire
- **3D Secure 2 (3DS2)** — authentication protocol for card-not-present transactions; mandated for SCA compliance in Europe
- **Strong Customer Authentication (SCA) / PSD2** — EU Payment Services Directive requiring two-factor authentication for online payments
- **NACHA / ACH** — US electronic funds transfer standards for bank-to-bank payment processing
- **Open Banking APIs (FDX, PSD2)** — enabling account-to-account payment initiation as an alternative to card networks

## Available Research Materials

1. Payments Dive (2025). *Adyen, Braintree and Stripe Face Off*. Payments Dive. https://www.paymentsdive.com/news/adyen-braintree-stripe-competition-digital-payments-merchants/691491/
2. Swell (2025). *30 High-Risk Payment Gateway Statistics Every Merchant Should Know in 2025*. Swell. https://www.swell.is/content/high-risk-payment-gateway-statistics
3. Tipalti (2025). *Ultimate Guide to Fraud Detection in Online Payments*. Tipalti. https://tipalti.com/resources/learn/fraud-detection-in-online-payments/
4. Microblink (2025). *Best Payment Processors in 2025: Secure, Scalable Payment Solutions for Fintechs*. Microblink Blog. https://microblink.com/resources/blog/best-payment-processors/
5. ChargeFlow (2025). *Stripe vs Adyen: The Most Reliable Comparison*. ChargeFlow Blog. https://www.chargeflow.io/blog/stripe-vs-adyen
6. Airwallex (2025). *Stripe vs Braintree Comparison: Which is Best for US Businesses?* Airwallex Blog. https://www.airwallex.com/us/blog/stripe-vs-braintree-comparison
7. ConnectPay (2026). *11 Best Online Payment Processing Services (2026)*. ConnectPay Blog. https://connectpay.com/blog/online-payment-processing-services/

## Market Research

**Market Size:** The global payment processing market is very large and growing rapidly. One analysis values the high-risk payment processing segment alone at USD 63.46 billion in 2025, growing to USD 214.8 billion by 2033 at a 13.5% CAGR. The broader payment infrastructure market encompasses trillions in transaction volume annually.

**Funding / M&A:** Stripe is valued at approximately USD 65–70 billion (last private round). Adyen is publicly listed with a market capitalisation of approximately USD 45 billion. Checkout.com raised at a USD 40 billion valuation in 2022 and has since adjusted. Airwallex is valued at approximately USD 6 billion. The sector continues to consolidate — Worldpay was spun out of FIS and is now independently operated.

**Pricing Landscape:** Consumer-facing processors (Square, Stripe standard) charge 2.6–2.9% + per-transaction fixed fees. Enterprise interchange++ pricing (Adyen, negotiated Stripe) starts in the range of interchange cost plus 0.1–0.3% processing mark-up. Volume discount thresholds vary; Braintree has been reported as low as 0.06% + $0.06 at very high volumes. Monthly platform minimums apply at Adyen.

**Key Buyer Personas:** CTOs and payments leads at e-commerce companies and SaaS platforms; CFOs at multi-national companies managing cross-border transaction costs; product managers at fintech companies embedding payments into applications; fraud and risk managers at large merchants managing chargeback rates.

**Notable Trends:** AI fraud detection is achieving 90% accuracy rates, with 71% of financial institutions now using AI-based systems. Multi-currency and alternative payment method (APM) support is table stakes for global merchants — 93% of international shoppers prefer local currency transactions. Account-to-account (A2A) payments via open banking are beginning to compete with card rails in Europe. Embedded finance — platforms becoming their own payment facilitators — is reshaping who controls the payment stack. Real-time payment networks (FedNow, RTP) are expanding US instant payment infrastructure.

## AI-Native Opportunity

- Real-time adaptive fraud scoring that evolves with new fraud patterns without requiring manual rule updates, using merchant-specific and network-wide signals simultaneously
- Intelligent chargeback management — predicting which disputes are worth fighting, auto-generating representment evidence, and identifying recurring fraud patterns by merchant category
- Dynamic currency optimisation — recommending the optimal processing currency and acquiring route for each transaction to minimise FX costs and interchange fees in real time
- Reconciliation automation — matching payment gateway records, bank statements, and accounting entries using AI to surface discrepancies without manual intervention, even across multiple currencies and payment methods
- Smart payment routing — directing transactions to the lowest-cost or highest-approval-rate processor in real time based on card type, issuer, geography, and historical authorisation data
