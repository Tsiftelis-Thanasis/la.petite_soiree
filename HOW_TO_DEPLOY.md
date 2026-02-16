# How to Deploy La Petite Soirée

This guide covers multiple deployment options for your website with Decap CMS.

## Prerequisites

- Your code pushed to GitHub (or GitLab/Bitbucket)
- A GitHub account

## Recommended: Deploy to Netlify (Free & Easy)

Netlify is the easiest option and works perfectly with Decap CMS.

### Step 1: Push Code to GitHub

```bash
# Make sure all files are committed
git add .
git commit -m "Add Decap CMS"

# Push to GitHub (if not already done)
git push origin master
```

### Step 2: Sign Up and Deploy to Netlify

1. Go to [Netlify](https://www.netlify.com/) and sign up (use GitHub account for easy login)

2. Click **"Add new site"** → **"Import an existing project"**

3. **Connect to Git provider:**
   - Choose **GitHub**
   - Authorize Netlify to access your repositories
   - Select your `la.petite_soiree` repository

4. **Configure build settings:**
   - **Branch to deploy:** `master`
   - **Build command:** Leave empty (no build needed for static site)
   - **Publish directory:** `/` (root directory)
   - Click **"Deploy site"**

5. **Wait for deployment** (usually 1-2 minutes)
   - You'll get a random URL like: `https://random-name-123456.netlify.app`

6. **Optional: Change site name**
   - Go to **Site settings** → **Site details** → **Change site name**
   - Choose something like: `lapetitesoiree` → `https://lapetitesoiree.netlify.app`

### Step 3: Enable Netlify Identity (Required for CMS)

1. In your Netlify site dashboard, go to the **"Identity"** tab

2. Click **"Enable Identity"**

3. **Configure registration:**
   - Under **"Registration preferences"**, select **"Invite only"** (recommended for security)

4. **Enable Git Gateway:**
   - Scroll to **"Services"** section
   - Click **"Enable Git Gateway"**
   - This allows the CMS to commit changes to your repository

### Step 4: Invite Yourself as a User

1. In the **Identity** tab, click **"Invite users"**

2. Enter your email address and click **"Send"**

3. Check your email for the invitation

4. Click the link in the email to set your password

### Step 5: Update Your Site with Identity Widget

Add the Netlify Identity widget to your `index.html`:

1. Open `index.html`

2. Add this code right before the closing `</body>` tag (line 388):

```html
<!-- Netlify Identity Widget -->
<script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>
<script>
  if (window.netlifyIdentity) {
    window.netlifyIdentity.on("init", user => {
      if (!user) {
        window.netlifyIdentity.on("login", () => {
          document.location.href = "/admin/";
        });
      }
    });
  }
</script>
```

3. Commit and push:
```bash
git add index.html
git commit -m "Add Netlify Identity widget"
git push origin master
```

4. Netlify will automatically redeploy (takes 1-2 minutes)

### Step 6: Access Your CMS

1. Go to: `https://your-site-name.netlify.app/admin/`

2. Click **"Login with Netlify Identity"**

3. Enter your email and password

4. You're in! Start editing content.

### Step 7: Disable Local Backend

Before final deployment, edit `admin/config.yml` and comment out local mode:

```yaml
# Uncomment below to enable local development mode
# local_backend: true
```

Commit and push this change.

---

## Alternative: Deploy to Vercel

Vercel is another excellent option (similar to Netlify).

### Quick Steps:

1. Go to [Vercel](https://vercel.com/) and sign up with GitHub

2. Click **"Add New"** → **"Project"**

3. Import your `la.petite_soiree` repository

4. Configure:
   - **Framework Preset:** Other
   - **Build Command:** Leave empty
   - **Output Directory:** Leave empty
   - Click **"Deploy"**

5. For authentication, you'll need to use GitHub OAuth (see `DECAP_CMS_SETUP.md`)

---

## Alternative: Deploy to GitHub Pages

Free hosting directly from GitHub.

### Steps:

1. **Enable GitHub Pages:**
   - Go to your repository on GitHub
   - Click **Settings** → **Pages**
   - Under **Source**, select **"Deploy from a branch"**
   - Choose **"master"** branch and **"/ (root)"** folder
   - Click **Save**

2. **Wait 2-3 minutes**, then visit: `https://your-username.github.io/la.petite_soiree/`

3. **Configure Decap CMS for GitHub:**
   - Edit `admin/config.yml`
   - Change backend to:
   ```yaml
   backend:
     name: github
     repo: your-username/la.petite_soiree
     branch: master
   ```

4. **Set up GitHub OAuth** (see `DECAP_CMS_SETUP.md` for detailed steps)

---

## Custom Domain (Optional)

### On Netlify:

1. Go to **Site settings** → **Domain management**

2. Click **"Add custom domain"**

3. Enter your domain (e.g., `lapetitesoiree.com`)

4. Follow instructions to update DNS records with your domain registrar

5. Netlify will automatically provision SSL certificate (HTTPS)

### On Vercel:

1. Go to **Settings** → **Domains**

2. Add your domain

3. Update DNS records as instructed

4. SSL is automatic

---

## Automatic Deployments

Once set up, deployments are automatic:

- **Any push to GitHub** triggers a new deployment
- **CMS edits** create commits, which trigger deployments
- **Takes 1-2 minutes** for changes to appear live
- **Preview deployments** available for branches/pull requests

---

## Environment Variables (If Needed Later)

If you add dynamic features later (contact forms, APIs), you can add environment variables:

### On Netlify:
1. Go to **Site settings** → **Environment variables**
2. Add key-value pairs

### On Vercel:
1. Go to **Settings** → **Environment Variables**
2. Add key-value pairs

---

## Monitoring Your Site

### Netlify:

- **Deploys:** See deployment history and logs
- **Analytics:** Enable Netlify Analytics (paid)
- **Forms:** Built-in form handling (free tier included)

### Vercel:

- **Deployments:** See deployment history
- **Analytics:** Enable Vercel Analytics (free tier included)
- **Logs:** View function logs (if using serverless)

---

## Troubleshooting

### Deployment fails
- Check the deployment logs in Netlify/Vercel
- Ensure all files are committed and pushed
- Verify no build errors

### Can't access /admin/
- Make sure `admin/` folder was deployed
- Check browser console for errors
- Try clearing browser cache

### CMS authentication not working
- Verify Netlify Identity is enabled
- Check that Git Gateway is enabled
- Ensure you accepted the invitation email
- Try logging out and back in

### Changes not appearing
- Wait 2-3 minutes for build to complete
- Check deployment status in dashboard
- Clear browser cache or try incognito mode

---

## Next Steps

1. ✅ Deploy to Netlify (or alternative)
2. ✅ Enable Netlify Identity and Git Gateway
3. ✅ Invite yourself as a user
4. ✅ Access CMS at `/admin/`
5. ✅ Start editing content!

See `NON_TECHNICAL_GUIDE.md` for instructions on how to edit content without coding knowledge.
