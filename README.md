# Peter van Onselen - Personal Website

A clean, modern personal website built with Jekyll and hosted on GitHub Pages.

## 🚀 Quick Start

This site is automatically deployed to GitHub Pages via GitHub Actions when you push to the `master` branch.

### Local Development

1. **Install dependencies:**
   ```bash
   bundle install
   ```

2. **Run the site locally:**
   ```bash
   bundle exec jekyll serve
   ```

3. **View the site:**
   Open your browser to `http://localhost:4000`

## 📁 Site Structure

```
├── _config.yml          # Site configuration
├── _layouts/            # HTML templates
│   ├── default.html     # Base layout
│   ├── page.html        # Page layout
│   └── post.html        # Blog post layout
├── _posts/              # Blog posts
│   └── 2025-08-01-welcome.md
├── assets/
│   ├── css/styles.css   # Custom styles
│   └── resume.pdf       # Your resume (to be added)
├── index.md             # Home page
├── about.md             # About page
├── projects.md          # Projects/Portfolio
├── blog.md              # Blog index
├── resume.md            # Resume page
├── contact.md           # Contact page
└── .github/workflows/   # GitHub Actions for auto-deployment
```

## 🛠 Customization

### 1. Update Site Information

Edit `_config.yml` to update:
- Site title and description
- Your social media links
- Navigation menu items

### 2. Add Your Content

**About Page (`about.md`):**
- Replace placeholder text with your actual LinkedIn information
- Add your education, work experience, and skills

**Projects Page (`projects.md`):**
- Add your actual projects from your portfolio
- Include GitHub links and live demo URLs

**Resume Page (`resume.md`):**
- Add your complete work history and skills
- Upload your PDF resume to `assets/resume.pdf`

**Contact Page (`contact.md`):**
- Add your actual email address
- Update social media links

### 3. Styling

The site uses a clean, professional design with:
- Responsive layout
- Modern typography (Inter font)
- Professional color scheme
- Mobile-friendly navigation

Customize the styles by editing `assets/css/styles.css`.

### 4. Blog Posts

Add new blog posts to the `_posts/` directory with the format:
```
YYYY-MM-DD-title.md
```

Each post should have frontmatter:
```yaml
---
layout: post
title: "Your Post Title"
date: 2025-08-01 10:00:00 +0000
categories: category1 category2
---
```

## 🚀 Deployment

The site automatically deploys to GitHub Pages when you:
1. Push changes to the `master` branch
2. GitHub Actions builds and deploys the site
3. Your site is available at `https://www.petervanonselen.com`

### Manual Deployment

If you prefer to build locally:
```bash
bundle exec jekyll build
```

## 📝 Next Steps

1. **Add your LinkedIn information** to all the placeholder sections
2. **Upload your resume PDF** to `assets/resume.pdf`
3. **Update contact information** with your actual email
4. **Add your project details** with real GitHub links
5. **Customize the styling** to match your preferences
6. **Write your first blog post** in `_posts/`

## 🔧 Troubleshooting

**Bundle install issues:**
- Make sure you have Ruby installed (preferably 3.1+)
- Try `bundle update` if packages are outdated

**Local build issues:**
- Check for typos in YAML frontmatter
- Ensure all required gems are installed
- Check Jekyll error messages for specific issues

**GitHub Pages deployment:**
- Ensure GitHub Pages is enabled in your repository settings
- Check the Actions tab for build errors
- Make sure the workflow has proper permissions

## 📞 Support

If you need help customizing this site, feel free to:
- Check the [Jekyll documentation](https://jekyllrb.com/docs/)
- Review [GitHub Pages documentation](https://docs.github.com/en/pages)
- Open an issue in this repository

---

**Built with ❤️ using Jekyll and GitHub Pages**
