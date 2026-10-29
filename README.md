# Next Step India — Education Consultancy Management System

This is a static web application designed for GitHub Pages + Supabase Free Tier.

## Included
- Email/password sign-in and staff account registration
- Admin/staff role model
- Student management with admission status, search and filters
- University directory (admin can add/delete)
- Scholarship tracking
- Supabase Row Level Security policies
- Mobile-friendly layout

## 1. Create database tables
1. Open your Supabase project.
2. Go to **SQL Editor** → **New query**.
3. Open `schema.sql`, copy all SQL, paste it into the editor, and click **Run**.
4. Confirm the script finishes without errors.

## 2. Configure the website
1. In Supabase, open **Project Settings → API Keys** (or the project's Connect/API area).
2. Copy the **Project URL** and the **Publishable key** (`sb_publishable_...`; legacy `anon` key can also work).
3. Open `index.html` in a text editor.
4. Find these lines near the bottom:
   ```js
   const SUPABASE_URL = "YOUR_SUPABASE_PROJECT_URL";
   const SUPABASE_PUBLISHABLE_KEY = "YOUR_SUPABASE_PUBLISHABLE_KEY";
   ```
5. Replace only the placeholder values. Do **not** use a `service_role` or secret key in this public website.
6. Save the file.

## 3. Publish on GitHub Pages (free)
1. Create a new GitHub repository, for example `next-step-india-management`.
2. Upload `index.html` to the repository root. Keep the filename exactly `index.html`.
3. Open repository **Settings → Pages**.
4. Under **Build and deployment**, choose **Deploy from a branch**.
5. Select branch `main` and folder `/(root)`, then **Save**.
6. Wait a few minutes. GitHub Pages will show your public website address under Settings → Pages.

## 4. Create the first admin
1. Open the published website.
2. Create an account with an email you control. If Supabase email confirmation is enabled, confirm the email first.
3. In Supabase, go to **SQL Editor** and run this query, replacing the email with your exact sign-up email:
   ```sql
   update public.profiles
   set role = 'admin', full_name = 'Next Step India Admin'
   where email = 'techman.rohit@gmail.com';
   ```
4. Verify the role:
   ```sql
   select id, email, role from public.profiles where email = 'techman.rohit@gmail.com';
   ```
5. Sign out and sign in again to refresh the session/UI.

**Important:** Only promote an account you personally control. Do not give staff access to your admin email/password.

## 5. Supabase Auth settings
- In **Authentication → URL Configuration**, add your GitHub Pages URL to **Site URL** and **Redirect URLs**.
- Use your exact published URL, for example `https://YOUR-USERNAME.github.io/YOUR-REPOSITORY/`.
- For a first test, email confirmation may remain enabled. Check your inbox/spam for the confirmation email.

## Notes and limitations
- The frontend is a starter implementation, not a fully audited production product.
- Staff can access only students and scholarship records assigned to their own user; admins can access all. University directory is visible to signed-in users and editable by admins.
- Staff account creation is open from the login page in this starter. If you do not want unapproved accounts, disable public sign-ups in Supabase Auth after creating your admin, then create staff users through a controlled admin workflow (a secure server-side function is needed for admin-created accounts).
- Student document uploads, PDF export, audit logs, password reset UI, admin staff management, and university/course application linking are not included yet; they can be added in the next iteration.
- Never store passwords, full payment-card details, or unnecessary sensitive information in student notes.
- Free tiers can change, and inactivity limits may apply. Check provider pricing and terms before relying on the app for critical operations.


## Admin account security
- The intended first administrator email is `techman.rohit@gmail.com`.
- First create that account from the website's sign-up screen, then confirm the email if required.
- Promote it to admin by running the SQL shown above.
- Do not hardcode an account password in `index.html` or any public GitHub repository. Set/change the password through Supabase Auth.
- If a real password was pasted into a chat or other shared place, change it immediately and do not reuse it.
