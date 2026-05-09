# Solleron POC Backlog (2-3 Months)

## Success Criteria
- Onboard at least 15 vendors and 100 buyers in pilot cohort.
- Complete at least 250 marketplace transactions.
- Achieve at least 30% of transactions using local currency in part or full.
- Keep checkout failure rate below 3%.
- Keep critical ledger inconsistencies at 0 unresolved incidents.

## Milestone Plan
### Milestone 1: Foundation Build (Weeks 1-4)
Goal: establish core data models and baseline marketplace flows.

### Milestone 2: Transaction + Currency Integration (Weeks 5-8)
Goal: deliver end-to-end purchasing with local currency support and admin controls.

### Milestone 3: Pilot Validation and Refinement (Weeks 9-12)
Goal: run live pilot, collect metrics, and finalize go/no-go recommendation.

## Prioritized Backlog
### M1 - Foundation Build
1. **User Accounts and Roles**
   - Buyer registration/login.
   - Vendor registration/login.
   - Admin role model.
   - Acceptance: users can authenticate and access role-specific views.

2. **Vendor Listing Management**
   - Create/edit/archive listings.
   - Add category, pricing, and availability metadata.
   - Acceptance: active listings appear in public browse view.

3. **Marketplace Browse**
   - Category-based listing browse.
   - Basic text search.
   - Acceptance: buyers can discover listings and view listing detail.

4. **Wallet and Ledger Schema**
   - Wallet per user/vendor.
   - Immutable transaction ledger entries.
   - Acceptance: every balance change maps to ledger events.

### M2 - Transaction and Currency Integration
5. **Checkout Flow**
   - Cart/checkout for listing purchase.
   - Payment split support (local currency + standard payment placeholder if needed).
   - Acceptance: order transitions from pending to completed with ledger updates.

6. **Currency Earn and Spend Rules**
   - Earn on eligible purchases.
   - Spend local currency on eligible listings.
   - Acceptance: balances update consistently according to rule set.

7. **Vendor Order Management**
   - Vendor view for incoming orders and status updates.
   - Acceptance: vendors can track and update fulfillment status.

8. **Admin Currency Controls**
   - Configure issuance rates and reward campaigns.
   - Flag suspicious activity for review.
   - Acceptance: config changes are auditable and reflected in transaction behavior.

### M3 - Pilot Validation and Refinement
9. **Analytics Dashboard (POC Scope)**
   - Track activation, transaction volume, currency usage, and failure rates.
   - Acceptance: weekly scorecard can be generated from dashboard data.

10. **Monitoring and Reliability**
    - Error logging for checkout and ledger pathways.
    - Alert on failed transactions and ledger write anomalies.
    - Acceptance: incidents can be detected and triaged quickly.

11. **Pilot Operations Playbook**
    - Vendor onboarding checklist.
    - Buyer onboarding communication template.
    - Support escalation process.
    - Acceptance: pilot team can run onboarding and support consistently.

12. **POC Final Evaluation**
    - Compare outcomes against success criteria.
    - Document lessons learned and scaling recommendations.
    - Acceptance: decision package ready for stakeholders.

## Risks and Contingencies
- **Low adoption**: run focused incentives and vendor co-marketing campaigns.
- **Ledger errors**: add reconciliation script and manual rollback protocol.
- **Scope creep**: freeze non-critical features after week 6.
- **Operational overload**: appoint pilot owner and weekly triage ritual.

## Definition of Done for POC
- All must-have flows are demonstrable end-to-end.
- Pilot metrics are captured and reviewed for at least 4 active weeks.
- Stakeholder readout includes outcomes, risks, and a clear recommendation.
