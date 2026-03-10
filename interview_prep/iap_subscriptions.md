# In-App Purchases (IAP) & Subscriptions

For a senior developer, IAP is more than just adding a plugin; it's about security, backend synchronization, and handling edge cases across platforms.

## 1. Types of Purchases

| Type | Description | Example |
| --- | --- | --- |
| **Consumable** | Used once, can be purchased multiple times. | Coins, health, hints. |
| **Non-Consumable** | Purchased once, stays with the user forever. | Pro version, premium filters. |
| **Auto-Renewing Sub** | Charges periodically until canceled. | Netflix sub, Monthly Pro. |
| **Non-Renewing Sub** | Fixed duration, no auto-renewal. | 1-year seasonal pass. |

## 2. The Verification Flow

### Client-Side Only (Basic)
1. User buys in app.
2. App receives "success" from store.
3. App unlocks content locally.
> [!CAUTION]
> **Extremely Insecure.** Vulnerable to "Local Receipt Override" tools. Only use for non-critical features.

### Server-Side (Senior Approach)
1. User buys in app.
2. App receives a **purchase receipt/token**.
3. App sends token to **your backend**.
4. Backend validates token with Google/Apple APIs.
5. Backend grants access in your DB and notifies the app.

## 3. Key Challenges & Senior Scenarios

### Restoring Purchases
Apple **requires** a "Restore Purchases" button for non-consumables/subscriptions. If you don't have it, your app will be rejected. 

### Grace Period & Account Hold (Sub-specific)
- **Grace Period:** Payment failed, but the user still has access (Store tries to re-bill).
- **Account Hold:** Payment failed, user access is revoked until they fix payment info.

### Churn & Refunds
How does your app react if a user refunds through the Google Play Store? 
- **Solution:** Use **Server-to-Server (S2S) Notifications**. The store sends a webhook to your server when a refund or cancellation happens.

## 4. Third-Party Solutions
Managing two different SDKs (StoreKit and Play Billing) is complex. Most seniors recommend abstractions:
- **RevenueCat:** The industry leader. Handles validation, webhooks, and cross-platform logic.
- **Qonversion / Glassfy:** Alternatives focusing on analytics and faster integration.

## 5. Security Checklist
- [ ] Never store secrets on the client side.
- [ ] Use `obfuscate` when building the app to hide strings.
- [ ] Implement receipt validation on your own server.
- [ ] Verify the `applicationId` / `bundleId` in the receipt matches your app.

---
> [!IMPORTANT]
> **Senior Tip:** If asked about IAP, mention **RevenueCat** vs **Custom Backend**. Explain that for a startup, RevenueCat is cost-effective, but for an enterprise, a custom backend provides better control over data and fees.

**Next Sitting Recommendation:** [App Lifecycle](./app_lifecycle.md) to manage resources when users leave the purchase screen.
