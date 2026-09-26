# Adagbor Descendant Association — website + API

## Website files

| File | Purpose |
|------|---------|
| `index.html` | Public site |
| `membership.html` | Membership application |
| `login.html` | Login |
| `dashboard.html` | Member area |
| `admin.html` | Admin area |
| `data-sync.js` | Auto-sync admin → members |
| `Adagbor.js` | **Cloudflare Worker API** (upload/deploy this) |

## Deploy API (`Adagbor.js`)

1. You already created `app_store` in D1 (done).
2. Optional for photos — in D1 Console:
   ```sql
   ALTER TABLE members ADD COLUMN photo TEXT;
   ```
3. Replace your Worker code with `Adagbor.js` and **Save & Deploy**.
4. Confirm bindings: `DB`, `ADMIN_KEY`, `RESEND_API_KEY`.

## Auto-sync (no JSON export)

Admin saves → `PUT /api/admin/store/:key` → D1 `app_store`  
Members/public → `GET /api/store/:key`

Keys used: `announcements`, `resolutions`, `attendance`, `payments`, `contribution_types`, `executives`
