# Pseudentity

**Deterministic Identity for Development.**

> [!CAUTION]
> **Early PoC Implementation** - This is an early proof-of-concept. APIs, architecture, and features can change significantly without prior notice. Not recommended for production use.

**Pseudentity** is the official visual companion and stateless Identity Provider for the [pseudata](https://github.com/pseudata/pseudata) ecosystem. It transforms the mathematical determinism of `pseudata` into a fully functioning, standards-compliant mock identity platform.

**[Live Demo: pseudentity.dev](https://pseudentity.dev)**

---

## Key Features

* **Profile Viewer:** Visualize any generated user with a rich UI, avatar, and metadata.
* **OpenID Connect Provider:** Add "Login with Pseudentity" to your apps. OIDC-compliant.
* **Mock Enterprise (SCIM 2.0):** Test user provisioning flows with infinite, paginated employee lists.
* **Mobile Ready:** Generate QR codes and **VCard (`.vcf`)** files to instantly populate mobile contacts.
* **The Factory API:** REST endpoints to generate consistent JSON data for any seed.

---

## Architecture

Pseudentity is **entirely stateless**. It uses CPU (Math) instead of Storage (Disk).

It relies on the **PseudoID**, a custom **UUID v8** that encodes the generation parameters directly into the 128-bit ID space. This allows any server to "inflate" a full user profile instantly just by decoding the ID, with zero database lookups.

**UUID v8 Layout:**
`SSSSSSSS-SSSS-8SSS-vSTT-TTIIIIIIIII`
* **Seed (64-bit):** The universe ID.
* **Type (16-bit):** Object type (User=101).
* **Index (40-bit):** Record position (0 to 1.1 Trillion).

---

## Getting Started

### Prerequisites
* Node.js 18+
* npm

### Installation

```bash
# Clone the repository
git clone [https://github.com/pseudata/pseudentity.git](https://github.com/pseudata/pseudentity.git)
cd pseudentity

# Install dependencies
npm install
```

### Development
Start the local Astro development server.

```bash
npm run dev
```
Visit `http://localhost:4321` to see the landing page.
Visit `http://localhost:4321/u/00000000-0000-8002-a806-5000000003e8` to see a sample profile.

---

## API Reference

### 1. Profile & Assets
Human-readable representations of an identity.

| Endpoint | Description |
| :--- | :--- |
| `GET /u/{uuid}` | **Profile Page** (HTML/Svelte). |
| `GET /u/{uuid}/data.json` | Raw user data (JSON). |
| `GET /u/{uuid}/avatar.png` | Deterministic avatar image. |
| `GET /u/{uuid}/cover.png` | Deterministic banner image. |
| `GET /u/{uuid}/contact.vcf` | **VCard 4.0** for mobile contact import. |

### 2. OpenID Connect Provider
Connect your application using standard OIDC libraries.

| Endpoint | Description |
| :--- | :--- |
| `/.well-known/openid-configuration` | Discovery document. |
| `/oidc/authorize` | Login endpoint (Enter Seed/UUID). |
| `/oidc/token` | Token exchange (Authorization Code). |
| `/oidc/userinfo` | Standard user profile endpoint. |
| `/oidc/jwks` | JSON Web Key Set (Public Keys). |

### 3. Enterprise (SCIM 2.0)
Mock endpoints for testing User Provisioning (Okta, Azure AD sync).

| Endpoint | Description |
| :--- | :--- |
| `/scim/v2/Users` | List users (supports `startIndex` & `count`). |
| `/scim/v2/Users/{id}` | Get specific SCIM user schema. |

---

## Deployment

This project is optimized for **Vercel Serverless**.

1.  **Fork** this repository.
2.  **Import** into Vercel.
3.  Set the Environment Variables (see below).
4.  Deploy.

### Environment Variables

| Variable | Description |
| :--- | :--- |
| `OIDC_SECRET` | A long, random string used to sign JWTs (HS256). |
| `OIDC_ISSUER` | The public URL of your instance (e.g., `https://pseudentity.dev`). |

---

## Contributing

We welcome contributions! Please see the [pseudata contribution guidelines](https://github.com/pseudata/.github/blob/main/CONTRIBUTING.md) for details on how to submit pull requests.

## License

This project is licensed under the **Apache 2.0 License** - see the [LICENSE](LICENSE) file for details.

---

<div align="center">
  <p>Part of the <a href="https://github.com/pseudata">Pseudata Ecosystem</a></p>
</div>