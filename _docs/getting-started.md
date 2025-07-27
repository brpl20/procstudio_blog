---
title: "Getting Started with ProcStudio"
category: "Setup & Installation"
date: 2024-12-28
author: "Development Team"
tags: [getting-started, setup, installation, basics]
excerpt: "Complete guide to getting started with ProcStudio development environment and basic workflows."
breadcrumbs: ["Setup & Installation", "Getting Started"]
related_docs: ["development-environment", "coding-standards"]
---

# Getting Started with ProcStudio

Welcome to the ProcStudio development documentation! This guide will help you set up your development environment and understand the basic workflows for contributing to the project.

## Prerequisites

Before you begin, ensure you have the following installed on your system:

- **Ruby** (version 2.7 or higher)
- **Bundler** gem
- **Node.js** (version 14 or higher)
- **Git**
- **Text Editor** (VS Code, Sublime Text, or similar)

## Initial Setup

### 1. Clone the Repository

```bash
git clone https://github.com/your-org/procstudio_blog.git
cd procstudio_blog
```

### 2. Install Dependencies

```bash
# Install Ruby gems
bundle install

# Install Node.js packages (if applicable)
npm install
```

### 3. Environment Configuration

Create a `.env` file in the root directory:

```env
JEKYLL_ENV=development
BUNDLE_GEMFILE=Gemfile
```

### 4. Start Development Server

```bash
bundle exec jekyll serve --livereload
```

Your site will be available at `http://localhost:4000`

## Project Structure

Understanding the project structure is crucial for effective development:

```
procstudio_blog/
├── _includes/          # Reusable HTML components
├── _layouts/           # Page templates
├── _posts/             # Blog posts
├── _docs/              # Private documentation (this system)
├── _sass/              # Stylesheet partials
├── assets/             # Static assets (CSS, JS, images)
├── docs/               # Public documentation route
├── img/                # Image assets
├── _config.yml         # Jekyll configuration
└── Gemfile             # Ruby dependencies
```

## Development Workflow

### Creating New Blog Posts

1. Create a new file in `_posts/` with the format: `YYYY-MM-DD-title.md`
2. Add the required front matter:

```yaml
---
layout: post
title: "Your Post Title"
subtitle: "Optional subtitle"
date: 2024-12-28 10:00:00 -0300
background: '/img/posts/your-image.jpg'
---
```

3. Write your content in Markdown
4. Test locally before committing

### Working with Assets

- **Images**: Place in `/img/` directory
- **Custom CSS**: Add to `_sass/` as partials
- **JavaScript**: Place in `/assets/js/`

### Git Workflow

1. Create a feature branch: `git checkout -b feature/your-feature`
2. Make your changes
3. Test thoroughly
4. Commit with descriptive messages
5. Push and create a pull request

## Common Tasks

### Adding New Pages

Create a new HTML or Markdown file in the root directory with front matter:

```yaml
---
layout: page
title: "Page Title"
description: "Page description"
background: '/img/bg-about.jpg'
---
```

### Customizing Themes

The project uses the Clean Blog theme. To customize:

1. Override theme files by creating matching files in your project
2. Modify `_sass/` files for styling changes
3. Update `_layouts/` for structural changes

### Performance Optimization

- Optimize images before adding them
- Use Jekyll's built-in Sass compilation
- Minimize custom JavaScript
- Test on mobile devices

## Troubleshooting

### Common Issues

**Bundle install fails**
```bash
# Update bundler and try again
gem update bundler
bundle install
```

**Jekyll serve errors**
```bash
# Clear cache and restart
bundle exec jekyll clean
bundle exec jekyll serve
```

**Live reload not working**
```bash
# Ensure you're using the --livereload flag
bundle exec jekyll serve --livereload --port 4000
```

### Getting Help

- Check the [Jekyll documentation](https://jekyllrb.com/docs/)
- Review existing code in the repository
- Ask team members for guidance
- Create an issue for bugs or feature requests

## Next Steps

Once you have the basic setup working:

1. Read the [Development Environment](development-environment) guide
2. Review our [Coding Standards](coding-standards)
3. Explore the [Deployment Process](deployment-process)
4. Check out [Advanced Features](advanced-features)

## Security Notes

- Never commit sensitive information (API keys, passwords)
- Use environment variables for configuration
- Keep dependencies updated
- Follow security best practices

---

*This documentation is part of our private internal knowledge base. Please keep it confidential and do not share outside the development team.*