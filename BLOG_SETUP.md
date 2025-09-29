# Blog Setup Guide for GitHub Pages

This guide explains how to add a blog section to your personal website hosted on GitHub Pages.

## Current Status

The blog section in `bbenson.html` has been commented out to hide it from the live site. To enable blogging, you have several options:

## Option 1: Simple HTML Blog (Easiest)

### Step 1: Enable the Blog Section
Uncomment the blog tab button and section in `bbenson.html`:
- Lines 114-116: Uncomment the blog tab button
- Lines 243-258: Uncomment the entire blog section

### Step 2: Add Blog Posts
Edit the blog section directly in `bbenson.html` by adding new posts in this format:

```html
<h3 class="text-xl sm:text-2xl font-semibold text-gray-800 mb-2">Your Post Title</h3>
<p class="text-gray-600 text-xs sm:text-sm mb-2">Published on: Date</p>
<p class="mb-4">Your post content preview...</p>
<a href="posts/your-post.html" class="text-blue-600 hover:underline">Read more...</a>
<hr class="my-6 border-gray-300">
```

### Step 3: Create Individual Post Pages
Create a `posts/` directory and add individual HTML files for each blog post:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Post Title - Bernard Benson</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-white text-gray-900 font-sans">
    <div class="max-w-4xl mx-auto p-6">
        <a href="../bbenson.html" class="text-blue-600 hover:underline mb-4 inline-block">&larr; Back to Home</a>
        <h1 class="text-3xl font-bold mb-4">Your Post Title</h1>
        <p class="text-gray-600 mb-6">Published on: Date</p>
        <div class="prose max-w-none">
            <!-- Your blog post content here -->
        </div>
    </div>
</body>
</html>
```

## Option 2: Jekyll Blog (More Advanced)

GitHub Pages supports Jekyll, which can generate a blog automatically from Markdown files.

### Step 1: Create Jekyll Configuration
Create `_config.yml` in your root directory:

```yaml
title: Bernard Benson
description: Research Scientist at NASA-IMPACT
baseurl: ""
url: "https://bernardbenson.github.io"

markdown: kramdown
highlighter: rouge
permalink: /:year/:month/:day/:title/

plugins:
  - jekyll-feed
  - jekyll-sitemap
```

### Step 2: Create Blog Layout
Create `_layouts/post.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ page.title }} - Bernard Benson</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-white text-gray-900">
    <div class="max-w-4xl mx-auto p-6">
        <a href="{{ site.baseurl }}/" class="text-blue-600 hover:underline mb-4 inline-block">&larr; Back to Home</a>
        <h1 class="text-3xl font-bold mb-4">{{ page.title }}</h1>
        <p class="text-gray-600 mb-6">Published on: {{ page.date | date: "%B %d, %Y" }}</p>
        <div class="prose max-w-none">
            {{ content }}
        </div>
    </div>
</body>
</html>
```

### Step 3: Create Blog Posts
Create posts in `_posts/` directory with format `YYYY-MM-DD-title.md`:

```markdown
---
layout: post
title: "Your Post Title"
date: 2025-07-14
---

Your blog post content in Markdown format.

## Subheading

Content with **bold** and *italic* text.
```

### Step 4: Update Main Page
Modify the blog section in `bbenson.html` to display Jekyll posts:

```html
<section id="blog" class="tab-content hidden">
    <h2 class="text-2xl sm:text-3xl font-bold text-gray-800 mb-4">My Blog</h2>
    <div class="prose max-w-none text-gray-700 text-base sm:text-lg">
        {% for post in site.posts limit:5 %}
        <h3 class="text-xl sm:text-2xl font-semibold text-gray-800 mb-2">
            <a href="{{ post.url }}" class="text-blue-600 hover:underline">{{ post.title }}</a>
        </h3>
        <p class="text-gray-600 text-xs sm:text-sm mb-2">Published on: {{ post.date | date: "%B %d, %Y" }}</p>
        <p class="mb-4">{{ post.excerpt }}</p>
        <hr class="my-6 border-gray-300">
        {% endfor %}
    </div>
</section>
```

## Option 3: External Blog Integration

### Embed Content from External Platforms
You can embed content from platforms like Medium, Dev.to, or your own blog:

```html
<div class="blog-embed">
    <script src="https://medium.com/feed/@yourusername"></script>
</div>
```

## Deployment

After making changes:

1. Commit your changes:
   ```bash
   git add .
   git commit -m "Add blog functionality"
   ```

2. Push to GitHub:
   ```bash
   git push origin gh-pages
   ```

3. Your changes will be live at your GitHub Pages URL within a few minutes.

## Tips

- **SEO**: Add meta tags to individual post pages for better search engine visibility
- **RSS Feed**: Jekyll automatically generates an RSS feed at `/feed.xml`
- **Comments**: Consider adding Disqus or GitHub Issues for comments
- **Analytics**: Add Google Analytics to track blog performance
- **Social Sharing**: Add social media sharing buttons to posts

## Recommended Approach

For a simple setup with minimal maintenance, **Option 1 (Simple HTML Blog)** is recommended. It gives you full control over styling and matches your existing site design perfectly.

For more advanced features like automatic post listing, tags, and RSS feeds, consider **Option 2 (Jekyll Blog)**.