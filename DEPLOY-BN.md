# দ্রুত Deploy

**সবচেয়ে সহজ flow:**
1. ZIP extract করুন।
2. GitHub-এ folder upload করুন।
3. Vercel → Add New Project → GitHub repo import।
4. PostgreSQL database তৈরি করুন।
5. Vercel Project Settings → Environment Variables:
   `DATABASE_URL`, `AUTH_SECRET`
6. Deploy।
7. Database schema apply করুন: `npx prisma db push` অথবা `database/schema.sql` চালান।

**নোট:** Database ছাড়া multi-device sync কাজ করবে না। একই account-এর data database-এ থাকে।
