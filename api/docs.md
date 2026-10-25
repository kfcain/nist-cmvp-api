# NIST CMVP API Reference

Static JSON API for NIST Cryptographic Module Validation Program data.

- **734** active validated modules
- **4,809** historical modules
- **185** modules in process
- **5,543** certificate detail records
- **1,925** certificates with algorithm summaries
- No auth required, unofficial project, GitHub Pages hosted.

Base URL: `https://kfcain.github.io/nist-cmvp-api/`

## Endpoints

### Index
`GET api/index.json` — API discovery endpoint with resource paths, documentation links, feature flags, and current counts.

### Metadata
`GET api/metadata.json` — Generation timestamp, source URLs, dataset counts, extraction metrics, and algorithm extraction status.

### JSON Schemas
`GET api/schemas/index.schema.json` — JSON Schema discovery document for the static API response files.

### Certificate Index
`GET api/certificates/index.json` — Compact discovery index for all 5,543 per-certificate detail files, including certificate numbers, datasets, paths, vendor/module names, statuses, standards, and algorithm counts.

### Search Indexes
`GET api/indexes/vendors.json`, `GET api/indexes/algorithms.json`, `GET api/indexes/statuses.json`, and `GET api/indexes/standards.json` — Split lookup files for common client-side search by vendor, algorithm, status, and standard.

### Data Quality
`GET api/data-quality.json` — Latest run quality report with misses, refreshed records, fallback usage, changed certificates, cache reuse checks, and the next scheduled weekly run.

### Changes
`GET api/changes.json` — Cumulative newest-first feed of added, removed, and summary-changed certificate numbers across recent weekly runs.

### Consumer Examples
`GET api/examples.json` — Copy-ready curl, Python, JavaScript, and agent-oriented query examples for vendor, module, algorithm, status, and standard lookups.

### Active Modules
`GET api/modules.json` — All 734 active validated modules.

Example response (truncated):

```json
{
  "metadata": {
    "generated_at": "2026-10-25T07:10:02.126598Z",
    "total_modules": 734
  },
  "modules": [
    {
      "Certificate Number": "5561",
      "Vendor Name": "Northrop Grumman Corporation",
      "Module Name": "Ad Noctem Connect 2.3",
      "Module Type": "Software",
      "Validation Date": "10/21/2026",
      "standard": "FIPS 140-3",
      "status": "Active",
      "overall_level": 1,
      "sunset_date": "10/20/2031",
      "algorithms": [
        "AES",
        "CVL",
        "DES",
        "DRBG",
        "ECDSA",
        "EDDSA",
        "HMAC",
        "KAS",
        "KDF",
        "RSA",
        "SHA"
      ],
      "security_policy_url": "https://csrc.nist.gov/CSRC/media/projects/cryptographic-module-validation-program/documents/security-policies/140sp5561.pdf",
      "certificate_detail_url": "https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/5561",
      "detail_available": true,
      "algorithm_extraction": {
        "schema_version": "1.0",
        "status": "parsed",
        "configured_source": "crawl4ai",
        "source": "crawl4ai",
        "source_url": "https://csrc.nist.gov/CSRC/media/projects/cryptographic-module-validation-program/documents/security-policies/140sp5561.pdf",
        "cached": false,
        "fallback_used": false,
        "cache_version": "2026-04-15-legacy-v1",
        "algorithm_count": 11,
        "detailed_algorithm_count": 39
      },
      "description": "The module is a VPN Client application. It provides secure communication over untrusted networks. To provide this security, the module implements IKEv2/IPsec...",
      "caveat": "When operated in approved mode. The module generates SSPs (e.g., keys) whose strengths are modified by available entropy."
    }
  ]
}
```

Each active module includes certificate identifiers, vendor/module names, validation metadata, direct Security Policy links, NIST detail URLs, detail availability flags, and algorithm extraction provenance when algorithms were evaluated.

### Historical Modules
`GET api/historical-modules.json` — All 4,809 expired or revoked modules for historical lookups.

### Modules In Process
`GET api/modules-in-process.json` — All 185 modules currently in the validation pipeline.

### Algorithms
`GET api/algorithms.json` — Algorithm usage summary across 1,925 certificates in the current build.

`algorithm_extraction` records the configured source, actual source, cache/fallback status, source URL, and extracted row counts for each evaluated certificate.

Example response (truncated):

```json
{
  "total_unique_algorithms": 19,
  "total_certificate_algorithm_pairs": 17422,
  "algorithms": {
    "AES": {
      "count": 1786,
      "certificates": [
        5551,
        5540,
        5550,
        5539,
        5549
      ]
    }
  }
}
```

### Certificate Details
`GET api/certificates/{certificate}.json` — Structured detail record for a specific certificate, including vendor/contact data, related files, validation history, and extracted algorithms when available.

Example response (truncated):

```json
{
  "metadata": {
    "generated_at": "2026-10-25T07:10:02.126598Z",
    "dataset": "active",
    "source": "https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/5551"
  },
  "certificate": {
    "certificate_number": "5551",
    "dataset": "active",
    "vendor_name": "Cisco Systems, Inc.",
    "module_name": "Cisco FTD FX-OS on 4K/9K Cryptographic Module",
    "standard": "FIPS 140-3",
    "status": "Active",
    "module_type": "Hardware",
    "overall_level": 2,
    "validation_dates": [
      "10/15/2026"
    ],
    "sunset_date": "10/14/2031",
    "caveat": "When operated in approved mode; The tamper evident seals and Physical Kit installed as indicated in the Security Policy; This module contains the embedded mo...",
    "security_level_exceptions": [
      "Roles, services, and authentication: Level 3",
      "Operational environment: N/A",
      "Non-invasive security: N/A"
    ],
    "vendor": {
      "name": "Cisco Systems, Inc.",
      "website_url": "http://www.cisco.com",
      "contact_email": "certteam@cisco.com"
    },
    "related_files": [
      {
        "label": "Security Policy",
        "url": "https://csrc.nist.gov/CSRC/media/projects/cryptographic-module-validation-program/documents/security-policies/140sp5551.pdf"
      }
    ],
    "validation_history": [
      {
        "date": "10/15/2026",
        "type": "Initial",
        "lab": "Gossamer Security Solutions"
      }
    ],
    "algorithms": [
      "AES",
      "CVL",
      "DRBG",
      "ECDSA",
      "HMAC"
    ],
    "algorithm_extraction": {
      "schema_version": "1.0",
      "status": "cached",
      "configured_source": "crawl4ai",
      "source": "crawl4ai",
      "source_url": "https://csrc.nist.gov/CSRC/media/projects/cryptographic-module-validation-program/documents/security-policies/140sp5551.pdf",
      "cached": true,
      "fallback_used": false,
      "cache_version": "2026-04-15-legacy-v1",
      "algorithm_count": 11,
      "detailed_algorithm_count": 59
    }
  }
}
```

Current build contains 5,543 certificate detail records across active and historical datasets.

## Workflows

### Discover the API surface
```
GET api/index.json → endpoints, docs links, feature flags, counts
GET api/metadata.json → freshness, scrape provenance, and extraction metrics
GET api/data-quality.json → latest run misses, refreshes, fallbacks, changed certs, and next scheduled run
GET api/changes.json → recent added, removed, and summary-changed certificate numbers
```

### Find a module and pull the full certificate record
```
GET api/certificates/index.json → discover every certificate detail path and summary row
GET api/modules.json → locate the certificate number or vendor/module pair
GET api/certificates/5551.json → full detail record for that certificate
```

### Check validation status and history for a certificate
```
GET api/certificates/5551.json → status, sunset_date, validation_history, related_files
```

### Explore algorithm coverage
```
GET api/algorithms.json → counts and certificate lists per algorithm
GET api/indexes/algorithms.json → compact certificate refs keyed by algorithm
GET api/modules.json → filter module rows by algorithms[] entries and inspect algorithm_extraction
```

## Caveats

- **Unofficial:** This project mirrors public CMVP data and is not affiliated with NIST. Use `https://csrc.nist.gov/projects/cryptographic-module-validation-program` for authoritative source material.
- **Static JSON:** There is no server-side filtering. Use the split search indexes or download the relevant JSON file and filter client-side.
- **CORS:** GitHub Pages does not send permissive CORS headers. Browser JavaScript on another origin will usually need a proxy.
- **404s:** Invalid certificate numbers or file paths return GitHub Pages' default 404 page at `https://kfcain.github.io/nist-cmvp-api`.
- **Algorithms coverage:** `api/algorithms.json` summarizes 1,925 certificates that had algorithm data in this build. `api/metadata.json` reports extraction cache hits, refreshes, failures, misses, and fallback counts.