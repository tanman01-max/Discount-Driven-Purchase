# DiscountIQ — GitHub Pages + Supabase

This version keeps the DiscountIQ dashboard on GitHub Pages and uses Supabase for real email/password authentication.

## 1. Create the Supabase project

Create a project at https://supabase.com/

Then open **Project Settings → API** and copy:
- Project URL
- Publishable key (or the legacy `anon` key if that is what your project shows)

**Never use the `service_role` / secret key in this website.**

## 2. Configure the site

Open `supabase-config.js` and replace:

```js
url: "YOUR_SUPABASE_PROJECT_URL",
publishableKey: "YOUR_SUPABASE_PUBLISHABLE_KEY"
```

with your values.

## 3. Configure email confirmation

Supabase email/password authentication is enabled by default. Hosted projects normally require email confirmation.

In Supabase:
**Authentication → URL Configuration**

Add your GitHub Pages URL as the Site URL / Redirect URL, for example:

`https://YOUR-GITHUB-USERNAME.github.io/YOUR-REPOSITORY/`

Also add that exact URL to the allowed redirect URLs if Supabase asks for it.

## 4. Upload to GitHub

The repository root should contain:

```text
index.html
supabase-config.js
.nojekyll
README.md
```

Then:

**Settings → Pages → Deploy from a branch → main → / (root) → Save**

## 5. What works

- Real Supabase signup
- Real email/password login
- Persistent Supabase sessions
- Logout
- Password reset email
- Email confirmation flow
- Your original DiscountIQ dashboard

Supabase Auth handles the passwords and sessions; the browser never needs a server-side secret.

## Optional database

You do not need a custom database table just to use login. Supabase Auth already manages authenticated users.

If you later want to save each user's DiscountIQ analyses, uploaded datasets, reports, or history, add Postgres tables with Row Level Security (RLS) so users can only access their own records.
