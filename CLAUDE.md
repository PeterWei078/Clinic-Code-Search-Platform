# CLAUDE.md

This file provides guidance when working with this repository.

## Project Overview

An interactive outpatient order search platform for common clinic medications, laboratory tests, imaging studies, procedures, injections/vaccines, and administrative documents. It reuses the single-file search/database-management architecture from the ICD-10 platform, but this repository is independent and should not be pushed to ICD-10-Platform.

## Running the App

This is a zero-build, single-file web application. Open `index.html` directly in any modern browser. No npm install, server, or build step is required.

## Architecture

The entire application lives in `index.html`. It uses CDN-loaded React 18, Babel standalone, Tailwind CSS, and Lucide icons.

## Data Shape

Each database entry uses this shape:

```js
{
  id: "LAB-HBA1C",
  code: "09006C",
  standard: "HbA1c",
  keywords: ["HBA1C", "A1C", "糖化血色素"],
  type: "exact" | "broad" | "context",
  organ: "Medication" | "Lab" | "Imaging" | "Procedure" | "Injection" | "Document" | "Other",
  note: "Optional local code guidance"
}
```

`code` may be an NHI code, hospital order code, medication code, or placeholder code. Replace sample codes with the actual clinic/HIS values when available.

## Key Constants

- `ORGAN_CATEGORIES`: order categories shown in filters and badges.
- `INITIAL_DATABASE`: built-in starter order database.
- `IGNORE_LIST`: non-order words ignored during batch analysis.

## Persistence

The app stores user-edited data in localStorage key `clinic_code_search_db`. This intentionally differs from the ICD-10 platform key so the two apps do not share browser data.

## Adding Entries

Add entries directly to `INITIAL_DATABASE` or use the app JSON import/export tools. Keep keywords rich: English name, abbreviation, Chinese name, brand name, local shorthand, and common misspellings if useful.
