## Windbnb

Full‑stack Airbnb‑style listing app built with Next.js 13 (App Router for UI, Pages Router for NextAuth), Prisma with MongoDB, Tailwind CSS, and Cloudinary uploads.

### Prerequisites
- Node.js 18+
- MongoDB connection string
- OAuth apps in Google and GitHub

### Environment
Create `.env` in the project root:

```env
DATABASE_URL=mongodb+srv://...
NEXTAUTH_SECRET=replace_with_random
NEXTAUTH_URL=http://localhost:3000

GITHUB_ID=your_github_client_id
GITHUB_SECRET=your_github_client_secret

GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret

NEXT_PUBLIC_CLOUDINARY_CLOUD_NAME=your_cloud_name
```

### Install & Run
```bash
pnpm install
pnpm dlx prisma generate
pnpm dev
```
Open `http://localhost:3000`.

### Auth Notes
- NextAuth runs from `pages/api/auth/[...nextauth].ts` (stable Pages Router).
- OAuth callback URLs must match your origin:
  - Google: `http://localhost:3000/api/auth/callback/google`
  - GitHub: `http://localhost:3000/api/auth/callback/github`
- If you change ports/host, update `NEXTAUTH_URL` and provider consoles, then clear cookies.

### Common Issues
- Tailwind not loading: ensure `postcss.config.js` and `tailwind.config.js` exist; restart dev server.
- Windows native bcrypt error: we use `bcryptjs`; do not install `bcrypt`.
- Image upload click error: handled by calling `widget?.open?.()` in `app/components/inputs/ImageUpload.tsx`.
- Listing page error: guarded missing `listingId` in `getListingById` to return `null`.

### Scripts
```json
{
  "dev": "next dev",
  "build": "next build",
  "start": "next start",
  "lint": "next lint"
}
```
