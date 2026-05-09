# Solleron Project Plan

## Vision Statement
Solleron is a community-driven marketplace for Solleron where local people and businesses can exchange goods and services using a locally developed currency, keeping value circulating inside the community.

## Problem Definition
Local communities often face three barriers:
- small local vendors struggle with visibility and repeat demand,
- residents buy outside the community because local discovery is fragmented,
- existing payment ecosystems do not directly reward local participation.

Solleron addresses these by combining a marketplace with a local currency that incentivizes local trade and strengthens community engagement.

## Stakeholders and Personas
- Community members (buyers): discover local offers, purchase with mixed payment options, earn local currency.
- Local sellers (vendors): list offerings, receive orders, accept local currency, build reputation.
- Community organizers/admins: manage trust and governance rules, monitor marketplace health.
- Project team: ships and operates the platform, validates adoption assumptions.

## Marketplace and Local Currency Concept
### Marketplace Core
- Vendor-managed listings (product/service, description, price, category, availability).
- Buyer browse, search, and checkout.
- Transaction history and basic dispute/reporting support.

### Local Currency Core
- **Earn**: users can earn local currency through defined actions (initially: purchases, participation campaigns, community contributions approved by admins).
- **Spend**: users can spend local currency for eligible marketplace purchases.
- **Ledger**: every currency movement is recorded in an auditable transaction ledger.
- **Governance**: simple, explicit issuance and redemption rules owned by community admins.

## Assumptions, Risks, and Constraints
### Assumptions
- At least 10-20 early vendors can be onboarded for pilot activity.
- Initial user base is willing to test a local currency model.
- A lightweight governance model is sufficient for POC trust.

### Risks
- Low early liquidity in local currency.
- Limited vendor adoption if onboarding effort is high.
- Abuse vectors (fake activity to farm currency).
- Regulatory ambiguity depending on the final currency model.

### Constraints
- POC targets validation over scale.
- Security, anti-fraud, and legal controls are minimal but explicit.
- Scope is limited to one community region and selected pilot participants.

## POC Scope
### Must Have (POC)
- User onboarding (buyer and vendor accounts).
- Listing creation and browsing.
- End-to-end transaction flow.
- Local currency wallet balances and transfer/usage in checkout.
- Basic admin panel for currency issuance rules and activity monitoring.
- Event logging and core analytics needed for success metrics.

### Later (Post-POC)
- Advanced recommendation/search ranking.
- Mobile apps (native).
- Complex governance workflows and voting.
- External payment provider optimization and settlement automation.

## Milestones and Timeline (2-3 Months)
### Month 1: Foundations
- Finalize requirement baseline and system boundaries.
- Implement auth, profile model, listing model, and browse experience.
- Design and implement ledger schema and wallet domain logic.

### Month 2: End-to-End Flows
- Implement checkout flow with local currency support.
- Implement vendor order management basics.
- Add admin controls for issuance and monitoring.
- Start pilot onboarding with a small user cohort.

### Month 3: Pilot Validation and Iteration
- Run structured pilot, measure adoption and transaction activity.
- Triage friction points and fix critical reliability issues.
- Produce final POC report and next-phase roadmap recommendation.

## Success Metrics and Validation
- Activation: number of onboarded vendors and active buyers.
- Usage: weekly active users and listing engagement.
- Currency utility: number and value of transactions using local currency.
- Retention: repeat buyers and repeat vendor transactions.
- Reliability: failed checkout rate, ledger integrity checks, incident count.

### Validation Approach
- Baseline metrics captured before pilot launch.
- Weekly scorecard reviewed by project team and community admins.
- End-of-POC decision based on adoption, reliability, and governance viability.

## Out of Scope for POC
- Full legal productionization of local currency framework.
- Enterprise-grade anti-fraud and compliance automation.
- Regional expansion outside initial Solleron pilot community.
