<p align="center">
  <a href="https://nakodax.com/data">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://nakodax.com/branding/nakodax-lockup.svg">
      <img alt="NakodaX" src="https://nakodax.com/branding/nakodax-lockup-on-light.svg" width="260">
    </picture>
  </a>
</p>

# NakodaX Data Pipelines: an encrypted codebase, left in public

**Our code is public. Our source isn't.**

![Encryption: AES-256-GCM](https://img.shields.io/badge/encryption-AES--256--GCM-00B26D) ![Protected files: 590](https://img.shields.io/badge/protected%20files-590-00B26D) ![Licence: proprietary](https://img.shields.io/badge/licence-proprietary-555) ![Warehouses: Snowflake and Databricks](https://img.shields.io/badge/warehouses-Snowflake%20%7C%20Databricks-555)

**We protect our own code with NakodaX. This repository is what that looks like from the outside.**

NakodaX Data Pipelines lets you share warehouse data with vendors, partners and customers while you keep control of it. This repository holds the Data Pipelines codebase, encrypted with NakodaX Source Protection. Clone it, open any file, and see what someone without a licence sees.

<p align="center">
  <img src="https://nakodax.com/illustrations/data-hero.webp" width="100%" alt="One data table seen through three frosted glass panes, each showing a different set of columns: NakodaX Data Pipelines gives each recipient their own view of shared data.">
</p>

[Product page](https://nakodax.com/data) · [Security at NakodaX](https://nakodax.com/security) · [Request review access](ACCESS.md) · [Unlock a protected app yourself: nkx-sample-app](https://github.com/nakodax/nkx-sample-app) · [Report a security issue](SECURITY.md)

## What is NakodaX Data Pipelines?

NakodaX Data Pipelines extracts data from your warehouse, applies protection, and shares it with the vendors, partners and customers who need it. Each recipient gets their own controlled view: only the rows and columns you allow, for as long as you allow. Access can be limited, expired or withdrawn after the data has been shared, and retention periods are enforced. The data stays in your environment and is never stored on NakodaX servers.

## What can you do with NakodaX Data Pipelines?

- **Share all data or only selected data**, and filter rows for each recipient.
- **Hide, mask or encrypt selected columns**, so sensitive fields never leave in readable form.
- **Give vendors, partners and customers their own view**, instead of one shared extract.
- **Set an expiry date** for access, and **enforce retention periods**.
- **End access when policy requires it**, not only when a contract ends.
- **Load protected data into a destination warehouse.**
- **Work with Snowflake and Databricks** without requiring Enterprise editions.
- **Keep data in your environment**, without storing it on NakodaX servers.

## This repository at a glance

| | |
|---|---|
| **Product** | NakodaX Data Pipelines, by NakodaX |
| **What this repository holds** | The Data Pipelines codebase: API service, pipeline engine, web console, warehouse connector and the DataGuard packages for Node, Python, Java and Spark |
| **What is protected** | 590 files: Python, TypeScript, TSX, Java and Scala source, plus tests, migrations, docs, scripts and config |
| **What stays readable** | Folder and file names, this README, `LICENSE`, `ACCESS.md`, `SECURITY.md`, `.gitignore`, and the `.nkx/manifest.json` files |
| **Protected with** | [NakodaX Source Protection](https://github.com/nakodax/nkx-source-protection) |
| **Encryption** | AES-256-GCM, with a separate random key for every file |
| **Key protection** | Each file key is wrapped with a key derived by scrypt (N = 2^17, r = 8, p = 1) and then bound to this build with HKDF-SHA256 |
| **Tamper resistance** | Every ciphertext is bound to its own file path, so renaming or swapping files makes decryption fail |
| **Encrypted files on disk** | `.nkxc`, one per protected file, plus companion stubs used by NakodaX tooling |
| **Licence** | Proprietary, public to inspect, not open source. See [`LICENSE`](LICENSE) |
| **Contact** | support@nakodax.com |

## How does NakodaX Data Pipelines work?

1. **Connect.** Point Data Pipelines at your warehouse. The data stays in your environment.
2. **Choose what to share.** Pick the tables, filter the rows for each recipient, and hide, mask or encrypt the columns they should not see.
3. **Share.** Each vendor, partner or customer gets their own protected view, or protected data loaded into their warehouse.
4. **Control.** Set expiry and retention. Change, limit or end a recipient's access at any time, including after the data has been shared.

## What can someone see in this repository without a key?

- **The layout.** Folder and file names are readable, as in any NakodaX protected repository.
- **Ciphertext.** Every `.nkxc` file is random-looking bytes. There is no code, comment or string to read.
- **The manifest.** `.nkx/manifest.json` lists each protected file with its wrapped key, its hashes and its language. Every file key in it is wrapped, and is useless without a valid NakodaX licence.
- **These documents:** this README, [`LICENSE`](LICENSE), [`ACCESS.md`](ACCESS.md), [`SECURITY.md`](SECURITY.md) and `.gitignore`.

## Check it yourself in one minute

```bash
git clone https://github.com/nakodax/nkx-data-protection.git
cd nkx-data-protection

# Count the encrypted files
git ls-files '*.nkxc' | wc -l

# Look inside one: random bytes, no source code
head -c 96 api/pipelines_api/main.py.nkxc | xxd

# Search every encrypted file for code keywords: no matches
grep -l -a -E '^(import|export|def|class|function) ' -r --include='*.nkxc' . | wc -l
```

**About this snapshot.** This repository is published as a single squashed commit of a protected release (November 2026). Development history and individual commits are not included in public snapshots.

## Who is NakodaX Data Pipelines for?

- **Data teams** that share datasets with vendors, partners or customers.
- **Companies with retention and data-residency obligations**, who need proof that shared data is deleted on time.
- **Anyone who needs to stop shared data being kept, copied or reused** after the agreement ends.
- **Teams already using a data clean room**, who also need to hand each partner a controlled view of their own.

## How is this different from other ways to share data?

| Approach | Recipient sees only their rows and columns? | Can access be ended after sharing? | Retention enforced? |
|---|---|---|---|
| **NakodaX Data Pipelines** | Yes, set per recipient | Yes, at any time | Yes |
| File exports (CSV, SFTP, email) | Only what you filtered by hand | No. Copies stay with the recipient | No |
| Shared warehouse credentials | Only if you build and maintain views per recipient | For future queries only | No |
| Contracts and DPAs alone | Whatever was sent | On paper only | On paper only |

## Frequently asked questions

### What is NakodaX Data Pipelines?

NakodaX Data Pipelines is a NakodaX product for sharing warehouse data with vendors, partners and customers under your control. It filters rows, protects columns, gives each recipient their own view, and lets you expire or end access after the data has been shared.

### Does NakodaX store my data?

No. The data stays in your environment and is never stored on NakodaX servers.

### Which warehouses does NakodaX Data Pipelines support?

Snowflake and Databricks, without requiring Enterprise editions. Protected data can also be loaded into a destination warehouse. See [nakodax.com/data](https://nakodax.com/data) for the current list.

### How is NakodaX Data Pipelines different from a data clean room?

It works alongside one. A clean room is built for joint analysis on shared data. Data Pipelines gives each partner their own controlled view, with row filters, column protection, expiry and retention, and access you can end at any time.

### Can I revoke access to data after it has been shared?

Yes. You can limit, expire or end a recipient's access at any time, including after the data has been shared.

### Is this repository open source?

No. It is public, not open source. You can clone it and read the five documents and the manifest. You may not decrypt, copy or redistribute the protected files, or use them to train AI models. See [`LICENSE`](LICENSE).

### Can an AI model or LLM read this repository?

No. Without a licence key, the protected files are ciphertext. An AI model, a code search index or a scraper learns nothing from them beyond file names.

### Can I build or run this repository?

Not without a key. To see NakodaX protected software unlock and run on your own machine, use [nkx-sample-app](https://github.com/nakodax/nkx-sample-app), which ships with a public trial licence.

### How do I get access to review the code?

Email **support@nakodax.com** with the subject `Source review: nkx-data-protection`. Customers, prospective customers, investors, auditors and security researchers with a specific question are reviewed case by case. [`ACCESS.md`](ACCESS.md) has the details.

## Key terms

- **Recipient view:** the rows and columns one vendor, partner or customer is allowed to see.
- **Retention period:** how long a recipient may keep shared data before it must be gone.
- **`.nkxc` file:** one source file's ciphertext. Useless without the manifest and a valid licence.
- **Manifest (`.nkx/manifest.json`):** the list of protected files, with each file's wrapped key and hashes.

## Related

- [nkx-source-protection](https://github.com/nakodax/nkx-source-protection): NakodaX Source Protection, the product that encrypts this repository, protected the same way
- [nkx-document-protection](https://github.com/nakodax/nkx-document-protection): NakodaX Document Protection, protected the same way
- [nkx-sample-app](https://github.com/nakodax/nkx-sample-app): see protection run, with a public trial key
- Website: [nakodax.com](https://nakodax.com) · Platform: [data.nakodax.com](https://data.nakodax.com) · Support: [nakodax.com/support](https://nakodax.com/support)

## Security and compliance

- **CSA STAR Level 1:** [listed on the CSA STAR Registry](https://cloudsecurityalliance.org/star/registry/nakodax-technologies-private-limited/services/nakodax), with our CAIQ answers public.
- **ISO/IEC 5230 and ISO/IEC 18974:** open source licence compliance and open source security assurance, [listed by OpenChain](https://openchainproject.org/community-of-conformance) ([announcement](https://openchainproject.org/news/2026/11/05/nakodax-announces-an-openchain-conformant-program)).
- **NIST CSF 2.0:** alignment across all 22 categories, updated every quarter.
- **NIST SSDF (SP 800-218):** our software development practices follow the Secure Software Development Framework.

Full details are on [nakodax.com/security](https://nakodax.com/security). For security documentation or a questionnaire, email security@nakodax.com.

## Security and licence

Found a problem? See [`SECURITY.md`](SECURITY.md). Proprietary, all rights reserved: [`LICENSE`](LICENSE).

*Last updated: November 2026.*
