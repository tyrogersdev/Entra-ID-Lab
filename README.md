# Entra ID – Access & ID Tokens Lab (My First Lab)

**Author:** Ty Rogers  
**Focus:** Microsoft Entra ID (OIDC), MSAL, Microsoft Graph `/me`  
**Note:** This is **my first ever lab**. I documented every step and included proof-of-work screenshots so anyone can follow and verify.

---

## Why I Did This
I wanted a hands-on way to learn **how sign-in works** (OIDC), the difference between **ID tokens** and **Access tokens**, and how to use **Microsoft Graph** with delegated permissions. Instead of just reading, I built a tiny app + walkthrough I can show to a hiring manager or mentor.

---

## Quickstart (TL;DR)
1. Register a web app in **Microsoft Entra ID** with redirect URI `http://localhost:5000/getAToken`.
2. Add delegated Microsoft Graph permission: `User.Read`.
3. Run the sample app (Flask/MSAL) and **sign in**.
4. View **decoded ID/Access token claims** and call **Graph `/me`**.
5. (Optional) Practice **PIM** role activation and access reviews.

---

## Prerequisites
- Microsoft Entra tenant + user account
- Python 3.10+ (if running the Flask/MSAL sample)
- Browser access to the **Entra admin center**

---

## Setup & Run (High Level)
- **App registration (Portal):**
  - New registration → **Single-tenant** → Redirect URI: `http://localhost:5000/getAToken`
  - Create a **client secret** (copy it once)
  - **API permissions** → Microsoft Graph (Delegated) → `User.Read`
- **Run app (example):**
  - Configure environment: `CLIENT_ID`, `TENANT_ID`, `CLIENT_SECRET`, `SCOPES=User.Read`
  - Start the app → browse to `http://localhost:5000` → **Login**
  - Inspect tokens and call `/me`

> If you’re not running the code, you can still follow the portal steps and map each step to the screenshots below.

---

## How It Works (Simple Architecture)
- **OIDC sign-in** with MSAL (Authorization Code + PKCE)
- **ID token** proves *who I am* (identity & claims)
- **Access token** proves *what I can do* (scopes/permissions)
- **Microsoft Graph** uses the access token to authorize `/me`
- **PIM** used to practice just-in-time (JIT) elevation and least privilege
- **Access Reviews** used to verify assignments and audit access

---

# Lab Evidence (Screenshots)

Below are the proof-of-work screenshots for the **Microsoft Entra ID – Access & ID Tokens Lab**.  
Each image is referenced with a brief caption. Replace any placeholder text with your own notes as needed.

![access review results](screenshots/access-review-results.png)

Screenshot 01: _Access Review results page._

![complete access review](screenshots/complete-access-review.png)

Screenshot 02: _Completed Access Review confirmation._

![PIM](screenshots/PIM.png)

Screenshot 03: _Privileged Identity Management (PIM) overview._

![Screenshot 2025-08-21 191935](screenshots/Screenshot%202025-08-21%20191935.png)

Screenshot 04: _Token decoding step._

![Screenshot 2025-08-21 192113](screenshots/Screenshot%202025-08-21%20192113.png)

Screenshot 05: _User assignment results._

![Screenshot 2025-09-08 222938](screenshots/Screenshot%202025-09-08%20222938.png)

Screenshot 06: _Graph API `/me` call._

![Screenshot 2025-09-09 171841](screenshots/Screenshot%202025-09-09%20171841.png)

Screenshot 07: _Role activation confirmation._

![Screenshot 2025-09-11 182549](screenshots/Screenshot%202025-09-11%20182549.png)

Screenshot 08: _Final access token validation._

---

## What I Learned (Key Takeaways)
- **ID vs Access token:** ID = authentication (who), Access = authorization (what + scopes).
- **Scopes & consent:** `User.Read` is required for Graph `/me`. Without the right scope, the call fails.
- **Redirect URI must match exactly** or you get `AADSTS50011`.
- **MSAL flow:** Authorization Code + PKCE is the secure web app standard.
- **PIM (JIT access):** Activate roles only when needed → least privilege in practice.
- **Access Reviews:** Periodically validate that the right users still have the right access.

---

## Troubleshooting (Real Errors I Hit)
- **AADSTS50011** – redirect mismatch  
  _Fix:_ Make sure the portal redirect URI is `http://localhost:5000/getAToken` (no trailing slash).
- **401 on Graph `/me`**  
  _Fix:_ Request `User.Read` and sign in again to get a fresh access token with that scope.
- **Images not showing in README**  
  _Fix:_ File path/extension mismatch; avoid extra spaces; use `![alt](<screenshots/file name.png>)` if there are spaces.

---

## Cleanup (Best Practice)
- Delete the **client secret** when done (Certificates & secrets).
- Remove the **app registration** if this was just a practice lab.
- Sign out and clear local tokens/cookies if you used a sample app.

---

## Next Steps (Future Labs I’ll Build)
- **Graph beyond `/me`**: list joined teams, mailbox basic info, or drive items.
- **RBAC deep dive**: custom roles, role assignments, and conditional access basics.
- **Detection rules**: create a simple KQL query for sign-in events + workbook.
- **Automate**: Terraform/Bicep for app reg + GitHub Actions to lint/validate.

---

## Repo Layout (Example)
