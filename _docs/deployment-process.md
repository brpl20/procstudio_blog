---
title: "Deployment Process"
category: "DevOps"
date: 2024-12-28
author: "DevOps Team"
tags: [deployment, devops, github-pages, ci-cd, production]
excerpt: "Complete deployment process documentation for ProcStudio Blog including CI/CD pipelines, environment management, and rollback procedures."
breadcrumbs: ["DevOps", "Deployment Process"]
related_docs: ["getting-started", "development-environment"]
---

# Deployment Process

This document outlines the complete deployment process for the ProcStudio Blog, including automated CI/CD pipelines, manual deployment procedures, and rollback strategies.

## Overview

The ProcStudio Blog is deployed using GitHub Pages with Jekyll, providing a robust and automated deployment pipeline. Our deployment strategy ensures zero-downtime deployments and maintains high availability.

### Deployment Architecture

```
GitHub Repository → GitHub Actions → GitHub Pages → CDN → Users
```

## Environments

### Production Environment
- **URL**: https://brpl20.github.io
- **Branch**: `main`
- **Auto-deploy**: Yes
- **Build time**: ~2-3 minutes

### Staging Environment
- **URL**: https://staging-brpl20.github.io (if configured)
- **Branch**: `staging`
- **Auto-deploy**: Yes
- **Purpose**: Pre-production testing

### Development Environment
- **URL**: http://localhost:4000
- **Branch**: Any feature branch
- **Purpose**: Local development and testing

## Automated Deployment (GitHub Actions)

### Main Deployment Workflow

The primary deployment is handled by GitHub Actions workflow located at `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout
      uses: actions/checkout@v3
      
    - name: Setup Ruby
      uses: ruby/setup-ruby@v1
      with:
        ruby-version: 3.0
        bundler-cache: true
        
    - name: Build Jekyll site
      run: |
        bundle exec jekyll build --destination _site
        
    - name: Deploy to GitHub Pages
      if: github.ref == 'refs/heads/main'
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./_site
```

### Deployment Triggers

Automatic deployments are triggered by:

1. **Push to main branch** - Production deployment
2. **Merge pull request** - Production deployment
3. **Manual workflow dispatch** - On-demand deployment

### Build Process

The build process includes:

1. **Environment Setup**
   - Ruby 3.0 installation
   - Bundler dependency installation
   - Node.js setup (if needed)

2. **Pre-build Checks**
   - Syntax validation
   - Link checking
   - Image optimization
   - Security scanning

3. **Jekyll Build**
   - Site generation
   - Asset compilation
   - Minification
   - SEO optimization

4. **Post-build Tasks**
   - Sitemap generation
   - RSS feed creation
   - Search index building

## Manual Deployment

### Emergency Deployment

For urgent fixes that bypass normal CI/CD:

1. **Prepare the fix**
   ```bash
   git checkout main
   git pull origin main
   git checkout -b hotfix/urgent-fix
   # Make your changes
   git add .
   git commit -m "hotfix: urgent production fix"
   ```

2. **Test locally**
   ```bash
   bundle exec jekyll serve
   # Verify fix works
   ```

3. **Deploy immediately**
   ```bash
   git checkout main
   git merge hotfix/urgent-fix
   git push origin main
   ```

### Manual Build and Deploy

If GitHub Actions is unavailable:

1. **Local build**
   ```bash
   export JEKYLL_ENV=production
   bundle exec jekyll build
   ```

2. **Deploy via GitHub CLI**
   ```bash
   gh-pages -d _site
   ```

## Pre-deployment Checklist

Before each deployment, ensure:

### Content Validation
- [ ] All new posts have proper front matter
- [ ] Images are optimized and properly sized
- [ ] External links are working
- [ ] Internal links are correct
- [ ] Meta descriptions are present

### Technical Validation
- [ ] Site builds without errors locally
- [ ] No broken Jekyll liquid tags
- [ ] CSS/JS assets are properly included
- [ ] Mobile responsiveness verified
- [ ] Performance tested

### SEO and Analytics
- [ ] Page titles are optimized
- [ ] Meta descriptions are unique
- [ ] Schema markup is valid
- [ ] Google Analytics tracking works
- [ ] Sitemap generates correctly

### Security Checks
- [ ] No sensitive information in repository
- [ ] Dependencies are up to date
- [ ] No security vulnerabilities detected
- [ ] Privacy policy is current

## Post-deployment Verification

### Automated Checks

Our deployment includes automated verification:

```bash
# URL availability check
curl -f https://brpl20.github.io || exit 1

# Performance check
lighthouse-ci --assert

# Link validation
htmlproofer ./_site --disable-external
```

### Manual Verification

1. **Smoke Tests**
   - Homepage loads correctly
   - Navigation menu works
   - Latest posts display
   - Contact form functions

2. **Cross-browser Testing**
   - Chrome/Chromium
   - Firefox
   - Safari (when possible)
   - Mobile browsers

3. **Performance Validation**
   - Page load times < 3 seconds
   - Core Web Vitals meet standards
   - Images load properly
   - CDN is functioning

## Rollback Procedures

### Immediate Rollback

If critical issues are detected post-deployment:

1. **GitHub Pages Rollback**
   ```bash
   # Revert to previous commit
   git revert HEAD
   git push origin main
   ```

2. **DNS/CDN Rollback**
   ```bash
   # If using custom CDN, rollback at CDN level
   # Contact hosting provider if needed
   ```

### Partial Rollback

For specific content issues:

1. **Content-only fixes**
   ```bash
   # Fix specific content
   git checkout main
   git revert <commit-hash> -- _posts/problematic-post.md
   git commit -m "rollback: remove problematic post"
   git push origin main
   ```

### Database Rollback

For configuration changes:

1. **Config rollback**
   ```bash
   git checkout main
   git revert <commit-hash> -- _config.yml
   git commit -m "rollback: revert config changes"
   git push origin main
   ```

## Environment Configuration

### Production Configuration

```yaml
# _config.yml (production)
url: "https://brpl20.github.io"
baseurl: ""
environment: production

# Performance optimizations
plugins:
  - jekyll-sitemap
  - jekyll-seo-tag
  - jekyll-compress-images

# Security headers
headers:
  - X-Frame-Options: DENY
  - X-Content-Type-Options: nosniff
  - X-XSS-Protection: "1; mode=block"
```

### Environment Variables

Set these in GitHub repository secrets:

- `GOOGLE_ANALYTICS_ID`: Google Analytics tracking ID
- `CONTACT_EMAIL`: Contact form email destination
- `CDN_URL`: CDN endpoint if using custom CDN
- `WEBHOOK_URL`: Deployment notification webhook

## Monitoring and Alerts

### Deployment Monitoring

- **GitHub Actions Status**: Monitor build/deploy success
- **Site Availability**: Uptime monitoring via UptimeRobot
- **Performance**: Google PageSpeed Insights integration
- **Error Tracking**: 404 error monitoring

### Alert Configuration

Set up alerts for:
- Build failures
- Site downtime (>2 minutes)
- Performance degradation (>5 second load time)
- 404 error spikes (>10% increase)

### Notification Channels

- **Slack**: #devops-alerts channel
- **Email**: dev-team@procstudio.com.br
- **SMS**: For critical production issues

## Troubleshooting

### Common Deployment Issues

**Build Failures**
```bash
# Check build logs
gh run list --workflow=deploy.yml
gh run view <run-id>

# Common fixes
bundle update
jekyll clean && jekyll build
```

**Asset Loading Issues**
```bash
# Verify asset paths
jekyll serve --verbose
# Check _site/ directory structure
```

**Caching Problems**
```bash
# Force refresh
curl -H "Cache-Control: no-cache" https://brpl20.github.io
# Clear GitHub Pages cache via GitHub support
```

### Performance Issues

**Slow Build Times**
- Optimize image sizes
- Remove unused plugins
- Use incremental builds for development

**Slow Page Loads**
- Enable compression
- Optimize images
- Minify CSS/JS
- Use CDN for assets

## Maintenance Windows

### Scheduled Maintenance

- **Weekly**: Dependency updates (Sundays, 2 AM UTC)
- **Monthly**: Security patches (First Sunday, 3 AM UTC)
- **Quarterly**: Major Jekyll version updates

### Emergency Maintenance

For critical security issues:
1. Immediate deployment authorization
2. Post-deployment communication
3. Incident report within 24 hours

## Documentation Updates

Keep deployment documentation current:

1. **Process Changes**: Update within 48 hours
2. **Tool Updates**: Document new versions/tools
3. **Lessons Learned**: Add troubleshooting sections
4. **Review Cycle**: Monthly documentation review

## Security Considerations

### Deployment Security

- All deployments use HTTPS
- No sensitive data in public repositories
- Regular dependency vulnerability scans
- Secure GitHub Actions workflow permissions

### Access Control

- **Repository**: Limited to development team
- **GitHub Actions**: Restricted to main branch
- **Secrets**: Encrypted and access-controlled
- **Production**: Read-only for most team members

---

*This deployment documentation is confidential and intended for the development and operations teams only. Follow all security protocols when deploying to production.*