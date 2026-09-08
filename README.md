# HISAB WEB — Multi-device Vercel Edition

এটি আপনার দেওয়া Android APK-এর দেখা feature/schema অনুযায়ী নতুন web implementation। APK নিজে Vercel-এ চালানো হয় না; এখানে Next.js web app তৈরি করা হয়েছে।

## কী আছে
- Account registration/login/logout
- একই account-এর জন্য cloud/server database data
- Customer add/edit/delete
- Billing/payment collection + due update
- Receipt + browser print
- Income / Expense
- Package management
- Categories
- Reports / due report
- Business settings
- Google Sheets webhook URL setting
- JSON backup export
- Mobile responsive UI

## Multi-device
একই account-এ দুই ফোন/কম্পিউটার থেকে login করলে data `/api/data` দিয়ে PostgreSQL database-এ shared থাকে। Browser localStorage-এ customer/payment data রাখা হয় না।

## Vercel deployment
1. একটি PostgreSQL database নিন (যেমন Neon/Supabase/Postgres provider)।
2. Database connection string কপি করুন।
3. Vercel-এ project import করুন বা GitHub-এ এই folder push করে import করুন।
4. Environment Variables দিন:
   - `DATABASE_URL` = PostgreSQL connection string
   - `AUTH_SECRET` = দীর্ঘ random secret
5. Deploy করুন। Build script Prisma client generate করে Next.js build করবে।
6. প্রথম deploy-এর আগে/পরে schema apply করুন: `npx prisma db push` (local terminal থেকে DATABASE_URL set করে) অথবা `database/schema.sql` SQL editor-এ চালান।

## Google Sheets
APK-তে পাওয়া Google Sheets sync structure-এর জন্য Customers/Payments/Expenses/Income data model রাখা হয়েছে। এই build-এ webhook URL setting আছে; পূর্ণ Google OAuth/service-account two-way sync চালু করতে আপনার Google credentials এবং কোন Sheet ব্যবহার করবেন তা লাগবে। Browser-এ service-account secret রাখবেন না।

## গুরুত্বপূর্ণ
এটি APK-এর source code copy নয়; APK inspection থেকে দেখা data model, screen/function names ও behavior অনুযায়ী clean web reimplementation। বর্তমান APK-এর private/local Room database data এই ZIP-এর ভিতরে নেই। সেই data দরকার হলে Room DB/export/Google Sheet আলাদা করে দিতে হবে।
