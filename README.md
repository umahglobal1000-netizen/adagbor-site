# Adagbor Descendant Association — website

## Files

| File | Purpose |
|------|---------|
| `index.html` | Public site |
| `membership.html` | Membership application |
| `login.html` | Login |
| `dashboard.html` | Member area |
| `admin.html` | Admin area |
| `data-sync.js` | Auto-sync admin → members (no manual export) |
| `worker-store-snippet.js` | Routes to add to your Cloudflare Worker |

## Automatic sync (no export)

Admin saves (announcements, resolutions, attendance, payments, executives, contribution types) are written to the API automatically. Members and the public page load the same data.

**One-time setup on the API worker**

1. In D1, run:
```sql
CREATE TABLE IF NOT EXISTS app_store (
  key TEXT PRIMARY KEY,
  value TEXT NOT NULL,
  updated_at TEXT NOT NULL
);
```

2. Add the GET `/api/store/:key` and PUT `/api/admin/store/:key` routes from `worker-store-snippet.js` to your existing worker (same `ADMIN_KEY` and `DB` binding).

Until those routes exist, data still saves on the admin device only (local fallback).

API: `https://adagbor-api.umahglobal1000.workers.dev`
