---
title: JJTeam Privacy Policy
---

# JJTeam Privacy Policy

**Effective date:** 2026-05-18
**Last updated:** 2026-05-18

JJTeam ("the App") establishes and discloses this Privacy Policy in accordance with Article 30 of the Personal Information Protection Act (Republic of Korea), to protect personal information of data subjects and to promptly and effectively handle related grievances.

The App provides two operation modes; the scope of personal information processed differs by mode.

- **Local mode (Start without sign-in):** All data is stored only on the user's device. No communication with external servers.
- **Cloud mode (Social sign-in):** After OAuth login, some data is stored on the operator's server to enable multi-device sync and real-time collaboration.

Users may choose either mode and can sign out or delete their account at any time to permanently delete server-side data.

---

## 1. Personal Information Processed

### 1.1 Local mode (all users)

The following information is stored only on the user's device in local storage (`AsyncStorage`).

- Team name
- Member name and grade (high/mid/low)
- Court and queue configuration
- Time thresholds, court count, court capacity, and other app settings
- Queue entry timestamps and other operational data

This data never leaves the user's device.

### 1.2 Cloud mode (users who sign in)

Upon social sign-in, the following items are received from OAuth providers (Google, Apple, Kakao) and stored on the operator's server.

- **Account identifiers**
  - Provider (google / apple / kakao)
  - Provider user ID (sub) — internal identifier, not displayed
  - Email (if shared by provider; may include Apple Hide My Email relay)
  - Display name (as set in the provider)
- **Authentication tokens**
  - JWT issued by the app (7-day validity, stored in device SecureStore)
  - Expo Push Token (optional, only if notification permission granted)
- **Team and session data**
  - Team name, members (name/grade/role: host|admin|member), court settings
  - Session data: queue, court slots, participants, guests
  - Session start/end times, queue entry timestamps
- **Anonymous spectators (non-members who join via QR)**
  - Display name entered at join
  - Anonymous token (valid for that session only)

### 1.3 Automatically collected information

- In cloud mode, standard HTTP metadata during API calls (IP address, User-Agent) — short-term logs for operational debugging
- Tokens routed via Expo Push infrastructure for notification delivery

The App does NOT use analytics, advertising, or crash-tracking SDKs. No advertising identifiers, cookies, or tracking pixels are used.

---

## 2. Purpose of Processing

Stored information is used only for the following purposes.

- **Local mode**
  - Restoring previous state when the user reopens the app
- **Cloud mode**
  - User identification and authentication via social sign-in
  - Multi-device synchronization of team/session data (including real-time WebSocket)
  - Session operation (court placement, queue management) and spectator viewing
  - Sending push notifications (only when permitted)

The App does NOT use personal information for marketing, advertising, profiling, or automated decision-making.

---

## 3. Retention and Use Periods

| Data | Storage | Retention |
|---|---|---|
| Local data (AsyncStorage) | User device | Until app removal or local mode exit |
| JWT / push token (SecureStore) | User device | Until sign-out or account deletion |
| Account / team / session (MongoDB Atlas) | Operator server (Korea region) | Until account deletion |
| Anonymous spectator data | Operator server | Auto-deleted at session end or by host |
| HTTP access logs | Operator server | Auto-deleted within 30 days |
| Revoked JWTs (Redis blocklist) | Operator server | Until token expiry (max 7 days) |

Upon account deletion, the user's account, teams (including teams they host), sessions, invite codes, and anonymous spectator records are permanently deleted.

---

## 4. Third-Party Disclosure

The operator does NOT disclose user information to any third party for advertising, marketing, or profiling purposes.

However, the following infrastructure providers process data on the operator's behalf. The scope and purpose are described in section 5.

- Google, Apple, Kakao (social sign-in)
- Google Cloud Platform (server hosting)
- MongoDB Atlas (database)
- Expo (push notification delivery)

---

## 5. Outsourcing of Processing

| Processor | Data | Purpose | Retention |
|---|---|---|---|
| Google LLC | OAuth ID token validation | Social sign-in | Validated at login only; not stored |
| Apple Inc. | Sign in with Apple token validation | Social sign-in | Same |
| Kakao Corp. | Kakao OIDC token validation | Social sign-in | Same |
| Google Cloud Platform (asia-northeast3, Seoul) | Server hosting | API/WebSocket/DB operation | Until account deletion |
| MongoDB Atlas | Database | Storage of account/team/session data | Until account deletion |
| Expo (650 California St., San Francisco, CA, USA) | Push tokens / delivery | Push notification routing | Until sign-out or token refresh |

Each processor follows its own privacy policy. The operator applies contractual safeguards to ensure data subject rights are preserved.

---

## 6. Deletion Procedures and Methods

- **Procedure**
  - Local data: Deleted immediately when the user chooses "Exit local mode" or removes the app
  - Cloud data: On "Delete account", the server transactionally removes the account, hosted teams, sessions, invites, and anonymous spectator records
  - Sign-out: Device JWT and anonymous tokens are deleted immediately, and the server registers the JWT in a revocation list
- **Method**
  - Local: Permanently deleted via the OS app-data deletion mechanism
  - Server: Permanently deleted from MongoDB Atlas. Backups are rotated and deleted within 7 days per operator policy

Users can delete their data by:

1. **Exit local mode** — Settings → Account → "Exit local mode"
2. **Sign out** — Settings → Account → "Sign out" (server data retained; device tokens revoked)
3. **Delete account** — Settings → Account → "Delete account" (both server and local data permanently deleted)
4. **Remove the app** — Delete the app from the device (only local data is deleted; cloud data remains)

---

## 7. Rights of Data Subjects

Under Articles 35-37 of the Personal Information Protection Act, users have the right to access, correct, delete, and suspend processing of their personal information.

- **Access:** In-app screens, or request via the contact in section 13
- **Correction:** Directly edit member name/grade in Team Settings
- **Deletion:** Use the "Delete account" method in section 6
- **Suspension:** Sign out or remove the app

For additional inquiries, contact the privacy officer in section 13.

---

## 8. Security Measures

- **Transport encryption:** All server communication uses HTTPS/WSS (TLS 1.2+).
- **Token security:** JWTs are stored in the device's OS secure storage (`SecureStore` — iOS Keychain / Android Keystore) and cannot be accessed by other apps.
- **Immediate revocation:** When a user signs out, the JWT is added to a server-side revocation list (Redis blocklist), invalidating it even if intercepted.
- **Minimum permission principle:** The app does NOT request camera, location, microphone, contacts, or photo permissions.
- **OAuth ID token verification:** Social sign-in ID tokens are verified directly using each provider's public keys.
- **No analytics/ads/crash SDKs:** The app does not include any SDK that tracks user behavior.

---

## 9. Automatic Collection (Cookies, etc.)

The App does NOT use cookies, advertising identifiers (IDFA/AAID), or tracking pixels.

---

## 10. Children Under 14

The App is not directed at children under 14 and does not knowingly collect personal information from them.

---

## 11. App Permissions

The App uses only the following OS permissions, all requiring explicit user consent.

- **Network access (internet):** For server communication in cloud mode (not used in local mode)
- **Push notifications (optional):** For session notifications from other hosts (only when user permits; not required for app functionality)

The App does NOT request camera, location, microphone, contacts, or photo permissions.

---

## 12. Cross-Border Transfer

The operator's server is located in the Korea region (Seoul). However, transfers outside Korea may occur in the following cases.

- **Expo push infrastructure:** Push notification tokens and payloads are routed via Expo servers in the United States. Notifications do not include personal information (e.g., "It's your turn").
- **OAuth providers:** During authentication with Google, Apple, or Kakao, the app accesses each provider's public-key endpoints for ID-token validation. No additional user data is transferred.

Transfer items, countries, dates, methods, recipients, purposes, and retention periods are disclosed throughout this policy. Users may refuse cross-border transfer by exiting cloud mode (cloud features become unavailable).

---

## 13. Privacy Officer

The app operator is responsible for personal information processing and grievance handling.

- **Name:** JJTeam Operator (No1Joon)
- **Email:** jjrottensweetpotato@gmail.com

Users may direct any inquiries, complaints, or remedy requests related to personal information to the above contact.

---

## 14. Remedies

Users may contact the following bodies for dispute resolution and counseling regarding personal information violations.

| Authority | Phone | Website |
|---|---|---|
| Personal Information Dispute Mediation Committee | 1833-6972 | www.kopico.go.kr |
| KISA Privacy Infringement Report Center | 118 | privacy.kisa.or.kr |
| Cyber Investigation Bureau, Supreme Prosecutors' Office | 1301 | www.spo.go.kr |
| Cyber Bureau, National Police Agency | 182 | ecrm.cyber.go.kr |

---

## 15. Policy Changes

If this Privacy Policy is added to, deleted from, or amended, the changes will be announced on this page at least 7 days before they take effect. For changes that materially affect user rights, notice will be given at least 30 days in advance.

---

## 16. Contact

For inquiries regarding this policy, please contact:

**Email:** jjrottensweetpotato@gmail.com
