# Next.js Blog System with GitHub Content Repository

## Overview

Production-ready blog system: Next.js 14 App Router + TypeScript + separate GitHub content repository.

**Architecture**: Complete separation between app code and content via GitHub API.

**Stack**: Next.js 14, TypeScript, Tailwind CSS, gray-matter + remark, ISR support.

## Key Directories

**App Repo**: `app/blog/`, `lib/blog.ts`, `types/`, `utils/`
**Content Repo**: `blog/*.md`, `images/heroes|screenshots|charts`, `videos/`

## Core Types

```typescript
// Essential interfaces
interface BlogPostFrontmatter {
  title: string; description: string; author: string
  date: string; category: BlogCategory; readTime?: string
  tags?: string[]; heroImage?: string; featured?: boolean
}

interface BlogPost extends BlogPostFrontmatter {
  slug: string; contentHtml: string; estimatedWordCount: number
}

type BlogCategory = 'Guides' | 'News' | 'Tools' | 'Analysis' | 'Getting Started' | 'Tutorial'

interface GitHubConfig {
  owner: string; repo: string; path: string; branch: string; token?: string
}
```

## Configuration

```bash
# Required env vars
NEXT_PUBLIC_GITHUB_OWNER=adapatandinnovate
NEXT_PUBLIC_GITHUB_REPO=ordx-blog-content
NEXT_PUBLIC_GITHUB_PATH=blog
GITHUB_TOKEN=ghp_your_token
```

```typescript
// lib/config.ts
export const GITHUB_CONFIG = {
  owner: process.env.NEXT_PUBLIC_GITHUB_OWNER || 'adapatandinnovate',
  repo: process.env.NEXT_PUBLIC_GITHUB_REPO || 'ordx-blog-content',
  path: process.env.NEXT_PUBLIC_GITHUB_PATH || 'blog',
  branch: 'main',
  token: process.env.GITHUB_TOKEN,
}

export const SITE_CONFIG = {
  title: 'Discovering Ordinals',
  description: 'All your Ordinals related content in one place!',
  author: 'Ord-X Team',
  siteUrl: 'https://ord-x.com',
}
```

## Core Functions

```typescript
// lib/blog.ts - Key functions
async function fetchFromGitHub<T>(endpoint: string): Promise<T> {
  const response = await fetch(
    `https://api.github.com/repos/${GITHUB_CONFIG.owner}/${GITHUB_CONFIG.repo}${endpoint}`,
    {
      headers: {
        Authorization: `token ${GITHUB_CONFIG.token}`,
        Accept: 'application/vnd.github.v3+json'
      },
      next: { revalidate: 300 }
    }
  )
  return response.json()
}

export async function getAllBlogPosts(): Promise<BlogPostPreview[]> {
  const files = await fetchFromGitHub('/contents/blog')
  return Promise.all(files.map(processMarkdownFile))
    .then(posts => posts.sort((a, b) => new Date(b.date).getTime() - new Date(a.date).getTime()))
}

export async function getBlogData(slug: string): Promise<BlogPost> {
  const file = await fetchFromGitHub(`/contents/blog/${slug}.md`)
  const content = Buffer.from(file.content, 'base64').toString()
  const { data, content: markdown } = matter(content)
  
  return {
    slug,
    contentHtml: await remark().use(html).process(markdown).then(String),
    estimatedWordCount: markdown.split(/\s+/).length,
    ...sanitizeFrontmatter(data, `${slug}.md`)
  }
}
```

## Content Validation

```typescript
// utils/validation.ts - Sanitize frontmatter with defaults
export function sanitizeFrontmatter(data: any, filename: string): BlogPostFrontmatter {
  const validCategories = ['Guides', 'News', 'Tools', 'Analysis', 'Getting Started', 'Tutorial']
  
  return {
    title: data.title || filename.replace('.md', '').replace(/-/g, ' '),
    description: data.description || 'No description provided',
    author: data.author || 'Unknown Author',
    date: data.date || new Date().toISOString().split('T')[0],
    category: validCategories.includes(data.category) ? data.category : 'Guides',
    readTime: data.readTime || '5 min read',
    tags: data.tags?.slice(0, 10) || [],
    heroImage: data.heroImage,
    featured: data.featured || false,
  }
}
```

## Caching

Next.js ISR handles caching automatically with `{ next: { revalidate: 300 } }` in fetch calls.

## Component Pattern

**Server Components** (data fetching): `app/blog/page.tsx`
**Client Components** (interactivity): `BlogListing.tsx` with useState/useMemo
**UI Components**: `BlogCard`, `CategoryBadge`, etc. in `components/`

## Content Format

**Required frontmatter**: `title`, `description`, `author`, `date`, `category`
**Optional**: `readTime`, `tags`, `heroImage`, `featured`
**Media**: GitHub raw URLs, organized in `images/heroes|screenshots|charts/`

```markdown
---
title: "Article Title"
description: "SEO description"
author: "Author Name"
date: "2024-01-15"
category: "Guides"
tags: ["tag1", "tag2"]
heroImage: "https://raw.githubusercontent.com/adapatandinnovate/ordx-blog-content/main/images/heroes/image.jpg"
featured: true
---

# Your Content Here
```

## Key Features

**Search**: Score posts by title/description/tags match  
**Performance**: ISR caching, build-time validation  
**SEO**: Dynamic sitemaps, structured data  
**Error Handling**: Fallbacks, validation, logging

## Dependencies

**Core**: `next@14`, `react@18`, `typescript@5`, `tailwindcss@3`  
**Content**: `gray-matter`, `remark`, `remark-html`  
**Config**: Enable GitHub image domains, ISR headers, TypeScript paths

## Workflow

1. **Setup**: App repo + content repo + GitHub API token
2. **Development**: TypeScript components + GitHub API integration
3. **Content**: Writers manage markdown files independently
4. **Deployment**: ISR + webhook triggers + validation

## Troubleshooting

**Rate Limits**: Add `GITHUB_TOKEN`  
**Build Issues**: Check env vars, validate frontmatter  
**Performance**: Use ISR, optimize API calls  
**TypeScript**: Verify interfaces, check path aliases

## Deployment

**Vercel**: Connect repo, add env vars, configure build  
**Security**: Use env vars for tokens, validate inputs, implement CSP

## Implementation Reference

**Testing**: Mock GitHub API, validate frontmatter, test components  
**Advanced Patterns**: `useContent` hook, error boundaries, HOCs  
**API Routes**: Search endpoint, analytics tracking  
**Automation**: GitHub Actions validation, webhook handlers  
**SEO**: Dynamic sitemap, structured data, performance metrics  
**Production**: Pre-deployment checks, health endpoints, monitoring

This system provides complete separation between app and content with full TypeScript safety.