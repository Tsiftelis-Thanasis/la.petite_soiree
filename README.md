# La Petite Soirée

A single-page website for La Petite Soirée - an elegant event planning and styling service specializing in intimate celebrations and curated events.

**Now with Content Management System (CMS) powered by Decap CMS!**

---

## 🎯 Current Status - Checkpoint

### ✅ Completed

- **Website Design:** Responsive single-page design with French-inspired aesthetic
- **CMS Integration:** Decap CMS installed and configured
- **Content Structure:** All content organized in manageable collections
- **Local Development:** Set up for testing CMS locally
- **Documentation:** Complete guides for deployment, content management, and non-technical users

### ⏳ Next Steps

1. Deploy to Netlify (see `HOW_TO_DEPLOY.md`)
2. Enable Netlify Identity for CMS authentication
3. Integrate content files with `index.html` (currently hardcoded)
4. Start managing content through the CMS

---

## 🌟 Features

### Website Features

- Responsive single-page design
- French-inspired elegant aesthetic
- Warm color palette (rose gold, blush pink, champagne, cream tones)
- Smooth scrolling navigation
- Service showcase section
- Gallery section
- Contact information with social links

### CMS Features

- **Visual Editor:** No coding required to update content
- **Content Collections:**
  - Site Settings (About text, contact info)
  - Services (Event planning cards)
  - Gallery (Photos and portfolio)
  - Blog & Portfolio (Future content)
- **Media Management:** Upload and manage images
- **Version Control:** All changes tracked in Git
- **Multi-user Support:** Invite team members to edit

---

## 🎨 Design

The site features a sophisticated color scheme with:

- Blush pink (#f4c2c2) and soft peach accents
- Rose gold (#b76e79) highlights
- Champagne (#f7e7ce) and cream (#fffbf3) backgrounds
- Warm taupe (#4a4238) typography

---

## 📁 Project Structure

```
la.petite_soiree/
├── index.html                    # Main website file
├── admin/                        # CMS admin interface
│   ├── index.html               # CMS entry point
│   └── config.yml               # CMS configuration
├── content/                      # All editable content
│   ├── settings.json            # Site-wide settings
│   ├── services/                # Service cards
│   ├── gallery/                 # Gallery items
│   └── blog/                    # Blog posts (future)
├── images/
│   └── uploads/                 # Uploaded media files
└── docs/                        # Documentation
    ├── HOW_TO_DEPLOY.md         # Deployment guide
    ├── HOW_CONTENT_UPDATES.md   # Technical workflow
    ├── NON_TECHNICAL_GUIDE.md   # For content editors
    ├── CMS_OPTIONS.md           # All CMS approaches
    ├── DECAP_CMS_SETUP.md       # Decap setup details
    └── LOCAL_DEVELOPMENT.md     # Local testing guide
```

---

## 🚀 Quick Start

### For Developers

**1. Clone the repository:**
```bash
git clone https://github.com/your-username/la.petite_soiree.git
cd la.petite_soiree
```

**2. Run locally (two terminals):**

Terminal 1 - Start CMS backend:
```bash
npx decap-server
```

Terminal 2 - Start web server:
```bash
npx http-server -p 8080
```

**3. Access:**
- Website: http://localhost:8080/
- CMS Admin: http://localhost:8080/admin/

### For Content Editors

See `NON_TECHNICAL_GUIDE.md` for complete instructions on managing content without coding knowledge.

---

## 📚 Documentation

| Guide | Description | For Whom |
|-------|-------------|----------|
| `HOW_TO_DEPLOY.md` | Deploy to Netlify, Vercel, or GitHub Pages | Developers |
| `HOW_CONTENT_UPDATES.md` | Technical details of content workflow | Developers |
| `NON_TECHNICAL_GUIDE.md` | Edit content without coding | Everyone |
| `CMS_OPTIONS.md` | All CMS approaches and future paths | Developers |
| `DECAP_CMS_SETUP.md` | Detailed Decap CMS setup | Developers |
| `LOCAL_DEVELOPMENT.md` | Run CMS locally | Developers |

---

## 🛠️ Technology Stack

- **Frontend:** HTML5, CSS3, Vanilla JavaScript
- **CMS:** Decap CMS (Git-based)
- **Content:** JSON + Markdown files
- **Version Control:** Git + GitHub
- **Hosting:** Netlify / Vercel / GitHub Pages (recommended)
- **Authentication:** Netlify Identity (recommended)

---

## 🔄 Content Management Workflow

```
Content Editor
    ↓
Edit in CMS (/admin/)
    ↓
Save/Publish
    ↓
Git Commit Created
    ↓
Automatic Deployment
    ↓
Live Site Updated (1-2 min)
```

---

## 📋 What You Can Edit Through CMS

### Site Settings
- Site title and tagline
- About section text (2 paragraphs)
- Contact information
- Social media links (Instagram, Email)

### Services
- Add/edit/delete service cards
- Change icons, titles, descriptions
- Reorder services

### Gallery
- Upload photos
- Add titles and descriptions
- Reorder gallery items
- Delete items

### Blog & Portfolio (Future)
- Write blog posts with rich text
- Upload featured images
- Add tags for organization
- Publish or save as drafts

---

## 🚀 Deployment Status

### Current State: Local Development ✅

### To Deploy:

1. **Push to GitHub:**
   ```bash
   git add .
   git commit -m "Add Decap CMS"
   git push origin master
   ```

2. **Deploy to Netlify:**
   - Follow steps in `HOW_TO_DEPLOY.md`
   - Enable Netlify Identity
   - Enable Git Gateway

3. **Access CMS:**
   - Go to `https://your-site.netlify.app/admin/`
   - Log in with Netlify Identity

4. **Start Editing:**
   - Manage content through visual interface
   - No coding required!

---

## ⚙️ Configuration

### CMS Configuration

Located in `admin/config.yml`:

- **Backend:** Git Gateway (for Netlify) or GitHub (for others)
- **Media Storage:** `images/uploads/` in repository
- **Collections:** Settings, Services, Gallery, Blog
- **Local Backend:** Enabled for local development

### To Switch to Production:

Edit `admin/config.yml` and comment out:
```yaml
# local_backend: true
```

---

## 🔐 Security

- **Authentication:** Netlify Identity (invite-only)
- **Git Gateway:** Secure proxy to GitHub
- **HTTPS:** Automatic with Netlify/Vercel
- **Version Control:** All changes tracked and revertable

---

## 🎯 Roadmap

### Phase 1: Basic CMS ✅
- ✅ Set up Decap CMS
- ✅ Configure content collections
- ✅ Create documentation
- ⏳ Deploy to Netlify
- ⏳ Enable authentication

### Phase 2: Content Integration (Next)
- [ ] Add JavaScript to load content dynamically
- [ ] OR migrate to static site generator (Astro recommended)
- [ ] Display blog posts on site
- [ ] Add blog listing page

### Phase 3: Advanced Features (Future)
- [ ] Contact form integration
- [ ] Image optimization
- [ ] SEO improvements
- [ ] Analytics integration
- [ ] Newsletter signup

### Phase 4: Scale (Optional)
- [ ] Migrate to headless CMS (Sanity/Contentful)
- [ ] Add e-commerce for event packages
- [ ] Client portal for event planning
- [ ] Online booking system

---

## 🤝 Contributing

### For Developers:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

### For Content:

1. Request access from site admin
2. Log in to CMS at `/admin/`
3. Edit content through visual interface
4. Changes auto-deploy to live site

---

## 📞 Contact & Support

- **Website:** https://your-site.netlify.app
- **Instagram:** [@la.petite_soiree](https://www.instagram.com/la.petite_soiree/)
- **Email:** hello@lapetitesoiree.com

### For Technical Issues:

- Check documentation in project root
- Review Decap CMS docs: https://decapcms.org/docs/
- Check Netlify support: https://answers.netlify.com/

---

## 📄 License

All rights reserved © 2026 La Petite Soirée

---

## 🙏 Acknowledgments

- **Decap CMS:** For the amazing Git-based CMS
- **Netlify:** For free hosting and authentication
- **Design Inspiration:** French elegance and sophistication

---

## 📝 Notes

### Important:

- **Content files are separate from HTML:** The CMS manages content in `content/` folder, but `index.html` is currently hardcoded. Integration needed to display CMS content on the site.

- **Local backend enabled:** Remember to disable `local_backend: true` in `admin/config.yml` before deploying to production.

- **Images in Git:** Uploaded images are stored in the repository. For large galleries, consider external media hosting (Cloudinary, etc.)

### Recent Changes:

- **2026-02-17:** Added Decap CMS with full documentation
- **2026-02-17:** Created content structure (Settings, Services, Gallery, Blog)
- **2026-02-17:** Set up local development environment

---

**Ready to launch!** Follow `HOW_TO_DEPLOY.md` to go live. 🚀
