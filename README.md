# Intune Error Database

A standalone, offline-capable browser tool for quickly looking up Microsoft Intune error codes, their causes, and step-by-step resolution guidance.

---

## Overview

The Intune Error Database is a single HTML file that runs entirely in the browser — no server, no installation, no internet connection required. It contains 75 documented Intune errors across 9 categories, each with a full error code, description, common causes, resolution steps, and a direct link to the relevant Microsoft Learn documentation page.

---

## Getting Started

1. Download `intune-error-db.html`
2. Open it in any modern browser (Chrome, Edge, Firefox, Safari)
3. No setup required — the tool is immediately usable

---

## Features

- **Category navigation** — left sidebar lists all error categories with entry counts; click any category to filter the list
- **Full-text search** — the search bar at the top searches across error codes, hex codes, titles, descriptions, causes, and resolution steps simultaneously
- **Detail view** — click any error card to open the full detail panel showing all fields
- **Microsoft Learn links** — each error links directly to the relevant official documentation page
- **Responsive layout** — adapts to any window size; the sidebar collapses on narrow screens with a back button for navigation
- **Fully offline** — all data is embedded in the HTML file; no external requests are made

---

## Error Categories

| Category | Errors | Description |
|---|---|---|
| Autopilot | 10 | Windows Autopilot deployment, ESP, profile assignment, TPM attestation |
| Applications | 12 | Win32 apps, MSI, Store apps, IME, detection rules, supersedence |
| Compliance | 8 | BitLocker, Defender AV, OS version, Secure Boot, firewall, passwords |
| Enrollment | 8 | Windows, iOS, Android enrollment, licensing, platform restrictions |
| Configuration | 10 | OMA-URI, certificates (SCEP/PKCS), Wi-Fi, VPN, email, update rings |
| Security | 7 | Security baselines, Conditional Access, LAPS, WHfB, MDE, ASR rules |
| Co-management | 3 | ConfigMgr/Intune co-management, workload switching, MDM authority |
| Device Management | 5 | Check-in failures, remote actions, wipe/retire, scope tags |
| Mobile | 5 | iOS APN/ABM/VPP, Android work profiles, Managed Google Play |
| Connectors | 4 | ODJ Connector, Certificate Connector, Exchange Connector, NPS Extension |

---

## Each Error Entry Contains

| Field | Description |
|---|---|
| **Error code** | Decimal or hex error code (e.g. `0x87D1041C`) |
| **Category** | Which Intune area the error relates to |
| **Title** | Short human-readable summary of the error |
| **Description** | Full explanation of what the error means and when it occurs |
| **Common causes** | Bulleted list of the most frequent root causes |
| **Resolution steps** | Numbered step-by-step remediation guide |
| **Documentation link** | Direct URL to the relevant Microsoft Learn page |

---

## How to Use

### Browsing by category
Click a category name in the left sidebar to filter the error list to that topic. Click **All errors** at the top of the sidebar to return to the full list.

### Searching
Type any of the following into the search bar to find matching errors:
- Error code (e.g. `0x80180014`)
- Hex code
- Keyword from the title or description (e.g. `BitLocker`, `TPM`, `certificate`)
- Text from a cause or resolution step (e.g. `NDES`, `manage-bde`, `dsregcmd`)

Up to 10 results are shown as a dropdown. Click any result to jump directly to that error's detail view.

### Viewing error details
Click any error card in the list to open the full detail panel on the right. The detail panel shows all fields for the selected error. On narrow screens, the detail view replaces the list — use the **← Back** button to return.

---

## Adding New Errors

The error data is stored as a JavaScript array inside the HTML file. To add new entries, open the file in a text editor, locate the `const DB=[` array, and append a new object following this structure:

```js
{
  id: 'unique_id',
  cat: 'Category Name',
  code: '0xXXXXXXXX',
  title: 'Short title of the error',
  desc: 'Full description of what the error means.',
  causes: [
    'First common cause',
    'Second common cause',
    'Third common cause',
  ],
  steps: [
    'First resolution step',
    'Second resolution step',
    'Third resolution step',
  ],
  url: 'https://learn.microsoft.com/en-us/mem/...'
}
```

**Guidelines for new entries:**
- `id` must be unique across all entries (suggested format: `cat###`, e.g. `ap011`, `comp009`)
- `cat` must exactly match an existing category name, or a new category will be created automatically in the sidebar
- `code` should be the full hex error code as it appears in Intune or Windows logs
- `causes` and `steps` should each have 3–5 entries for consistency
- `url` should point to the most relevant Microsoft Learn page for the error

Alternatively, share the error details in a conversation with Claude and request an updated HTML file — the new entries will be added and a fresh file generated for download.

---

## Technical Details

| Property | Value |
|---|---|
| File type | Single HTML file |
| Dependencies | None (no external libraries or CDN calls) |
| Browser support | All modern browsers (Chrome 90+, Edge 90+, Firefox 88+, Safari 14+) |
| Internet required | No — fully offline capable |
| Data storage | Embedded in HTML (JavaScript array) |
| Total entries | 75 errors |

---

## Known Limitations

- Error data reflects knowledge available as of the tool's creation date; new Intune errors released by Microsoft after that date will not be present until manually added
- The tool does not sync with any live Microsoft database or API
- There is no built-in export or print function; use the browser's built-in print/save-as-PDF feature if a printed reference is needed
- The search does not support wildcard operators or boolean logic; it performs a simple substring match across all fields

---

## File Reference

```
intune-error-db.html    — the complete tool (open this in a browser)
intune-error-db-docs.md — this documentation file
```
