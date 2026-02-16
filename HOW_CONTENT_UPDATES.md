# How Content Updates Work

This document explains the technical workflow of how content updates flow from the CMS to your live website.

## Overview

```
Content Editor (You)
    ↓
Decap CMS Interface (/admin/)
    ↓
Commit to GitHub Repository
    ↓
Automatic Deployment Triggered
    ↓
Live Website Updated
```

---

## The Content Workflow

### 1. Content Storage

Content is stored in your Git repository as files:

```
content/
├── settings.json          # Site-wide settings
├── services/              # Service cards
│   ├── event-planning.md
│   ├── styling-design.md
│   └── intimate-celebrations.md
├── gallery/               # Gallery items
│   ├── elegant-decor.md
│   ├── table-settings.md
│   └── ...
└── blog/                  # Blog posts (future)
    └── 2026-02-17-my-first-post.md
```

**Why files?**
- Version controlled (track all changes)
- No database needed (simpler, more secure)
- Easy to backup (just the Git repo)
- Portable (works anywhere)

### 2. Editing Content

**When you edit in Decap CMS:**

1. You open: `https://your-site.netlify.app/admin/`

2. You navigate to a collection (Services, Gallery, Settings, etc.)

3. You make changes in the visual editor

4. You click **"Save"** or **"Publish"**

**What happens behind the scenes:**

```
Decap CMS
    ↓
Authenticates with Netlify Identity
    ↓
Calls Git Gateway API
    ↓
Creates a commit to your GitHub repo
    ↓
Changes saved to content files
```

### 3. Git Commits

**Each save creates a Git commit:**

```bash
# Example commit created by CMS:
commit abc123def456
Author: Your Name <you@email.com>
Date: Mon Feb 17 10:30:00 2026

    Update Services "event-planning"

    - Changed description text
```

**What this means:**
- Full history of all changes
- Can revert to any previous version
- Can see who made what changes
- Professional version control

### 4. Automatic Deployment

**When a commit is pushed to GitHub:**

1. **Netlify/Vercel detects the change** (via webhook)

2. **Deployment starts automatically**
   - Downloads latest code
   - Copies files to CDN
   - No build step needed (static site)

3. **Takes 1-2 minutes**

4. **Live site updates** with new content

**Deployment logs show:**
```
✓ Cloning repository
✓ Preparing files
✓ Publishing to CDN
✓ Deploy successful!
```

---

## Content File Formats

### JSON Files (settings.json)

```json
{
  "siteTitle": "La Petite Soirée",
  "tagline": "Curated Events & Intimate Celebrations",
  "aboutText1": "Your about text here...",
  "email": "hello@lapetitesoiree.com"
}
```

**Used for:** Simple key-value settings

### Markdown Files (services, gallery, blog)

```markdown
---
title: Event Planning
icon: 🎉
description: Complete event coordination...
order: 1
---

Optional body content here (for blog posts)
```

**Structure:**
- **Frontmatter** (between `---`): Metadata (title, date, etc.)
- **Body** (after `---`): Main content (for blog posts)

**Used for:** Content collections with metadata

---

## How CMS Connects to GitHub

### Authentication Flow:

```
You log in
    ↓
Netlify Identity authenticates you
    ↓
Decap CMS requests Git access
    ↓
Git Gateway (Netlify service) authenticates with GitHub
    ↓
CMS can read/write to your repository
    ↓
You can edit content
```

**Security:**
- Git Gateway acts as a proxy (secure)
- Only invited users can access CMS
- OAuth tokens are encrypted
- No GitHub credentials stored in CMS

---

## Current State: Static HTML

**Important:** Right now, your `index.html` has **hardcoded content**.

### Current Flow:
```
Edit in CMS → Content files update → Deployment happens
BUT
index.html still shows hardcoded text
```

### What You See in CMS vs Website:

| Location | Status |
|----------|--------|
| `/admin/` (CMS) | ✅ Can edit content files |
| `/` (Website) | ❌ Shows hardcoded HTML |

### To Connect Them:

You need to either:

**Option A: Add JavaScript to load content**
```html
<script>
  // Fetch content/settings.json
  // Update page dynamically
</script>
```

**Option B: Use a Static Site Generator**
- Convert to Astro, 11ty, or Next.js
- Templates pull from content files at build time
- Recommended for blog functionality

See `CMS_OPTIONS.md` for details on these approaches.

---

## Media Management

### Image Uploads:

1. **Upload in CMS:**
   - Click image field
   - Upload file
   - Select from media library

2. **File stored in:**
   ```
   images/uploads/your-image.jpg
   ```

3. **Committed to Git:**
   ```bash
   git add images/uploads/your-image.jpg
   git commit -m "Upload your-image.jpg"
   ```

4. **Reference in content:**
   ```markdown
   ---
   image: /images/uploads/your-image.jpg
   ---
   ```

### Image Storage Options:

**Current (Default):**
- ✅ Images stored in Git repository
- ✅ Simple, no external services
- ❌ Repo can get large with many images

**Alternative (Advanced):**
- Use Cloudinary or Uploadcare
- Images stored externally
- Automatic optimization
- See Decap CMS docs for setup

---

## Draft vs. Published

For blog posts, you can control publishing:

```yaml
---
title: My Post
published: false  # Draft - not visible
---
```

**Workflow:**
1. Create post with `published: false`
2. Write and preview
3. When ready, change to `published: true`
4. Your static site generator can filter by this field

---

## Content Workflow Best Practices

### For Solo Editor (You):

1. **Edit directly in CMS**
   - No need for Git knowledge
   - Make changes and save
   - See changes live in 1-2 minutes

### For Multiple Editors (Team):

1. **Use editorial workflow** (enable in config)
   ```yaml
   publish_mode: editorial_workflow
   ```

2. **Three stages:**
   - **Draft:** Work in progress
   - **In Review:** Ready for review
   - **Ready:** Approved, ready to publish

3. **Creates branches and pull requests**
   - Each draft is a separate branch
   - Approve to merge to master
   - Automatic deployment after merge

---

## Monitoring Changes

### View in GitHub:

1. Go to your repository

2. Click **"Commits"**

3. See all CMS edits with:
   - Who made the change
   - What changed
   - When it happened

### View in Netlify:

1. Go to **"Deploys"** tab

2. See:
   - Deployment status
   - Trigger (CMS edit, push, manual)
   - Deployment time
   - Preview URL

---

## Rollback Changes

If you need to undo changes:

### Method 1: Via GitHub

1. Find the commit before your change
2. Click **"Revert"** button
3. Automatic deployment with old content

### Method 2: Via CMS

1. Re-edit the content
2. Change back to previous values
3. Save

### Method 3: Via Git (Advanced)

```bash
# View history
git log

# Revert specific commit
git revert abc123

# Push to trigger deployment
git push
```

---

## Performance Considerations

### Static Files = Fast

- No database queries
- Files served from CDN
- Cached globally
- Sub-second page loads

### Build Time

**Current:** ~10 seconds
- Just copying files

**With Static Site Generator:** ~30-60 seconds
- Generating HTML from templates
- Processing markdown
- Optimizing images

Still very fast compared to dynamic sites!

---

## Scaling Considerations

### Current Setup Can Handle:

- ✅ Up to ~100 pages
- ✅ Hundreds of images
- ✅ Multiple editors
- ✅ Millions of visitors

### When to Upgrade:

**Move to Static Site Generator when:**
- Adding a blog with 10+ posts
- Need better image optimization
- Want dynamic content features
- Need advanced templates

**Move to Headless CMS when:**
- Need real-time collaboration
- 5+ content editors
- Content used in multiple apps
- Need advanced workflows

---

## Summary

### Current Workflow:
1. ✅ Edit in CMS (`/admin/`)
2. ✅ Save creates Git commit
3. ✅ Automatic deployment
4. ⏳ Need to integrate with `index.html` (next step)

### Benefits:
- No database to manage
- Free hosting (Netlify/Vercel)
- Automatic backups (Git history)
- Fast and secure

### Next Steps:
- See `HOW_TO_DEPLOY.md` to go live
- See `NON_TECHNICAL_GUIDE.md` to start editing
- See `CMS_OPTIONS.md` to integrate content with HTML

