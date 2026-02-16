# Decap CMS Setup Guide

Decap CMS has been added to your La Petite Soirée website! This guide will help you get started.

## What is Decap CMS?

Decap CMS is a Git-based content management system that adds a user-friendly admin interface at `/admin` to edit your site content. All content changes are saved as commits to your Git repository.

## Quick Start

### Step 1: Enable Netlify Identity (Recommended Authentication)

The easiest way to set up authentication is using Netlify:

1. **Deploy to Netlify** (if not already deployed)
   - Push your code to GitHub
   - Go to [Netlify](https://www.netlify.com/) and sign in
   - Click "Add new site" → "Import an existing project"
   - Connect to GitHub and select your repository
   - Deploy settings:
     - Build command: (leave empty)
     - Publish directory: `/`

2. **Enable Netlify Identity**
   - In your Netlify site dashboard, go to "Identity" tab
   - Click "Enable Identity"
   - Under "Registration preferences", select "Invite only" (recommended)
   - Under "Services" → "Git Gateway", click "Enable Git Gateway"

3. **Invite yourself as a user**
   - Click "Invite users" in the Identity tab
   - Enter your email address
   - Check your email and accept the invitation

4. **Add Netlify Identity Widget to your site**
   - Add this script to your `index.html` before the closing `</body>` tag:
   ```html
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

### Step 2: Access the CMS

1. Visit your site at: `https://your-site.netlify.app/admin/`
2. Log in with your Netlify Identity credentials
3. Start editing content!

## Alternative: GitHub OAuth (For Advanced Users)

If you prefer GitHub authentication instead of Netlify Identity:

1. Create a GitHub OAuth App:
   - Go to GitHub Settings → Developer settings → OAuth Apps
   - Create new OAuth App
   - Set Homepage URL to your site URL
   - Set Authorization callback URL to: `https://api.netlify.com/auth/done`

2. Add OAuth credentials to Netlify:
   - In Netlify dashboard: Settings → Access control → OAuth
   - Install GitHub provider
   - Enter Client ID and Client Secret from GitHub OAuth App

3. Update `admin/config.yml`:
   ```yaml
   backend:
     name: github
     repo: your-username/la.petite_soiree
     branch: master
   ```

## Local Development (Optional)

To run Decap CMS locally and test changes before deploying:

1. Install the Decap CMS proxy server:
   ```bash
   npx decap-server
   ```

2. Uncomment this line in `admin/config.yml`:
   ```yaml
   local_backend: true
   ```

3. Access the CMS at: `http://localhost:8080/admin/`

4. When done, comment out `local_backend: true` before deploying

## Content Structure

Your content is organized in the following folders:

### `/content/settings.json`
Site-wide settings including:
- Site title and tagline
- About section text
- Contact information
- Social media links

### `/content/services/`
Each service is a markdown file with:
- Title
- Icon (emoji)
- Description
- Display order

### `/content/gallery/`
Gallery items with:
- Title
- Image (optional - can upload through CMS)
- Alt text
- Display order

### `/content/blog/`
Blog posts and portfolio entries with:
- Title
- Date
- Featured image
- Description and full content
- Tags
- Published status

## Content Management Features

### What You Can Do:

1. **Edit Site Settings**
   - Update about text
   - Change contact information
   - Modify social media links

2. **Manage Services**
   - Add new services
   - Edit existing service descriptions
   - Change service icons
   - Reorder services

3. **Update Gallery**
   - Upload images
   - Add new gallery items
   - Edit titles and descriptions
   - Reorder gallery items

4. **Create Blog Posts**
   - Write new posts with markdown
   - Upload featured images
   - Add tags for organization
   - Save as draft or publish immediately

### Workflow:

1. **Edit Content** in the CMS interface
2. **Save** creates a commit to your repository
3. **Publish** triggers a deployment (on Netlify/Vercel)
4. Changes appear on your live site automatically

## Media Management

- Upload images through the CMS interface
- Images are stored in `/images/uploads/`
- Automatic image optimization (when using Netlify/Vercel)
- Images are committed to your Git repository

## Next Steps

### Current Setup:
- ✅ CMS interface configured
- ✅ Content structure created
- ✅ Collections defined (Settings, Services, Gallery, Blog)
- ⏳ Authentication needed (follow Step 1 above)
- ⏳ Integrate content into HTML (see below)

### To Display CMS Content on Your Site:

Currently, your `index.html` has hardcoded content. You'll need to either:

**Option A: Use JavaScript to load content** (Keep current HTML file)
- Add JavaScript to fetch and display content from JSON/markdown files
- Works with static hosting
- Simple to implement

**Option B: Use a Static Site Generator** (Recommended for blog)
- Convert to Astro, 11ty, or Next.js
- Better for blogs and complex content
- See `CMS_OPTIONS.md` for details

Would you like help implementing either option?

## Troubleshooting

### Can't access /admin/
- Make sure you deployed the `admin/` folder
- Check that `admin/index.html` and `admin/config.yml` exist
- Clear browser cache

### Authentication issues
- Verify Netlify Identity is enabled
- Check that Git Gateway is enabled
- Confirm your email is invited

### Changes not appearing
- Check that commits are being created in your repo
- Verify deployment is triggering on Netlify/Vercel
- Wait a few moments for build to complete

## Resources

- [Decap CMS Documentation](https://decapcms.org/docs/)
- [Netlify Identity Setup](https://docs.netlify.com/visitor-access/identity/)
- [Content Modeling Guide](https://decapcms.org/docs/collection-types/)

## Support

For issues specific to:
- **Decap CMS**: Check [GitHub Issues](https://github.com/decaporg/decap-cms/issues)
- **Netlify Identity**: Check [Netlify Support](https://answers.netlify.com/)
- **This setup**: Refer to `CMS_OPTIONS.md` for alternative approaches
