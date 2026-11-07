# Commonroom

A small, responsive community forum built with React, TypeScript, Vite, and Supabase. It includes email/password registration and sign-in, discussion channels, new topics, replies, and row-level security. Without Supabase credentials the site runs in a read-only preview mode with sample discussions.

## Run locally

1. Install Node.js 22 or later.
2. Install dependencies and start the development server:

   ```sh
   npm install
   npm run dev
   ```

3. Copy `.env.example` to `.env.local` and set your Supabase project URL and publishable key.

## Connect Supabase

1. Create a Supabase project.
2. In the Supabase SQL Editor, run [`supabase/schema.sql`](./supabase/schema.sql). It creates the profile, topic, and reply tables, their access policies, and a profile-on-sign-up trigger.
3. In **Authentication → URL Configuration**, add your local URL and deployed GitHub Pages URL to the allowed redirect URLs.
4. The supplied Supabase project URL and publishable key are configured in the ignored `.env.local` for local development. For another project, set those values in `.env.local`. Do not put a service-role key in the website.

Email confirmation may be enabled in Supabase. When it is, new members must confirm their email before signing in.

## Deploy on GitHub Pages

1. Push this project to a GitHub repository, using `main` as its default branch.
2. In **Settings → Secrets and variables → Actions**, create repository secrets named `VITE_SUPABASE_URL` and `VITE_SUPABASE_PUBLISHABLE_KEY`. Use the supplied project URL and publishable key.
3. In **Settings → Pages**, set the source to **GitHub Actions**.
4. Push to `main` or run **Deploy forum to GitHub Pages** from the Actions tab. The workflow builds the app with the Supabase secrets and deploys `dist`.
5. Add the final Pages URL to the Supabase allowed redirect URLs.

The Supabase URL and publishable key are public client configuration embedded in the site at build time. Database security comes from the row-level security policies; never use a Supabase service-role key in a browser build.
