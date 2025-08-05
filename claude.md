# TypeScript Next.js Blog System with Separate GitHub Content Repository

## Project Overview

This is a production-ready blog system built with Next.js 14 App Router and TypeScript that maintains complete separation between application code and content. The system fetches blog content from a separate GitHub repository via the GitHub API, enabling independent workflows for developers and content creators.

## Architecture Principles

### Repository Separation Strategy
- **Main Application Repository**: Contains all frontend code, components, utilities, and build configuration
- **Content Repository**: Contains only markdown files, images, videos, and media assets
- **Zero Overlap**: No content in app repo, no code in content repo
- **API Bridge**: GitHub API connects the two repositories during build and runtime

### Technology Stack
- **Framework**: Next.js 14 with App Router
- **Language**: TypeScript with strict type checking
- **Styling**: Tailwind CSS with Typography plugin
- **Content Processing**: Gray-matter + Remark for markdown
- **Deployment**: Vercel/Netlify compatible with ISR support

## File Structure

### Main Application Repository Structure
```
nextjs-blog-ts/
├── app/
│   ├── blog/
│   │   ├── [slug]/
│   │   │   ├── page.tsx                 # Individual post page (Server Component)
│   │   │   ├── BlogPost.tsx             # Post content (Client Component)
│   │   │   ├── loading.tsx              # Post loading state
│   │   │   └── not-found.tsx            # 404 for missing posts
│   │   ├── BlogListing.tsx              # Interactive blog listing (Client)
│   │   ├── page.tsx                     # Blog index (Server Component)
│   │   ├── loading.tsx                  # Blog loading state
│   │   └── error.tsx                    # Blog error boundary
│   ├── components/
│   │   └── BlogComponents.tsx           # All reusable UI components
│   ├── globals.css                      # Tailwind CSS imports
│   ├── layout.tsx                       # Root layout with metadata
│   ├── page.tsx                         # Homepage
│   ├── loading.tsx                      # Global loading component
│   └── error.tsx                        # Global error boundary
├── lib/
│   ├── blog.ts                          # GitHub API integration functions
│   └── config.ts                        # Configuration and validation
├── types/
│   ├── blog.ts                          # Blog-related type definitions
│   └── github.ts                        # GitHub API type definitions
├── utils/
│   ├── cache.ts                         # Type-safe caching utilities
│   ├── validation.ts                    # Content validation functions
│   ├── performance.ts                   # Performance tracking
│   └── search.ts                        # Advanced search functionality
├── public/
│   └── images/                          # App static assets only
├── .env.local                           # Environment variables
├── .env.example                         # Environment template
├── package.json                         # Dependencies and scripts
├── tsconfig.json                        # TypeScript configuration
├── tailwind.config.ts                   # Tailwind configuration
├── postcss.config.js                    # PostCSS configuration
├── next.config.js                       # Next.js configuration
└── README.md                            # Developer documentation
```

### Content Repository Structure
```
ordx-blog-content/
├── blog/                                # Markdown articles only
│   ├── bitcoin-ordinals-guide.md
│   ├── wallet-setup-tutorial.md
│   ├── defi-analysis-2024.md
│   └── nft-marketplace-review.md
├── images/                              # Image assets organized by type
│   ├── heroes/                          # Large featured images
│   │   ├── bitcoin-ordinals-hero.jpg
│   │   └── wallet-setup-hero.png
│   ├── screenshots/                     # UI screenshots
│   │   ├── metamask-install.png
│   │   └── uniswap-interface.jpg
│   ├── charts/                          # Data visualizations
│   │   ├── bitcoin-price-chart.svg
│   │   └── defi-tvl-growth.png
│   └── misc/                            # Other images
│       ├── author-avatars.png
│       └── company-logos.svg
├── videos/                              # Video content
│   ├── tutorials/                       # Tutorial videos
│   │   ├── wallet-setup-demo.mp4
│   │   └── defi-staking-guide.mp4
│   └── animations/                      # Animated content
│       └── blockchain-explainer.gif
├── docs/                                # Content guidelines
│   ├── writing-style-guide.md
│   └── markdown-template.md
├── .gitignore                           # Git ignore rules
└── README.md                            # Content team documentation
```

## Core Type Definitions

### Blog Content Types
```typescript
// types/blog.ts
export interface BlogPostFrontmatter {
  title: string
  description: string
  author: string
  date: string                           # YYYY-MM-DD format
  readTime?: string                      # e.g., "5 min read"
  category: BlogCategory
  tags?: string[]
  heroImage?: string                     # Full URL to image
  featured?: boolean
  seoKeywords?: string[]
  difficulty?: BlogDifficulty
  lastUpdated?: string
  tableOfContents?: boolean
  newsletter?: boolean
  comments?: boolean
  socialSharing?: boolean
}

export interface BlogPost extends BlogPostFrontmatter {
  slug: string
  contentHtml: string                    # Processed HTML from markdown
  estimatedWordCount: number
}

export interface BlogPostPreview extends BlogPostFrontmatter {
  slug: string                           # Used for routing
}

export type BlogCategory = 
  | 'Guides' 
  | 'News' 
  | 'Tools' 
  | 'Analysis' 
  | 'Getting Started'
  | 'Tutorial'

export type BlogDifficulty = 'Beginner' | 'Intermediate' | 'Advanced'

export interface SearchResult extends BlogPostPreview {
  score: number
  excerpt?: string
}
```

### GitHub API Types
```typescript
// types/github.ts
export interface GitHubConfig {
  owner: string                          # GitHub username/org
  repo: string                           # Content repository name
  path: string                           # Folder containing markdown files
  branch: string                         # Branch to fetch from
  token?: string                         # Optional auth token
}

export interface GitHubFile {
  name: string
  path: string
  sha: string
  content?: string                       # Base64 encoded content
  encoding?: 'base64'
  type: 'file' | 'dir'
  download_url: string
}

export interface CacheEntry<T> {
  data: T
  timestamp: number
  ttl: number
}
```

## Configuration Management

### Environment Variables
```typescript
// .env.example
NEXT_PUBLIC_GITHUB_OWNER=your-github-username
NEXT_PUBLIC_GITHUB_REPO=your-content-repository-name
NEXT_PUBLIC_GITHUB_PATH=blog
NEXT_PUBLIC_GITHUB_BRANCH=main
GITHUB_TOKEN=ghp_your_github_personal_access_token
NEXT_PUBLIC_SITE_URL=https://your-domain.com
NEXT_PUBLIC_SITE_NAME="Your Blog Name"
```

### Configuration with Validation
```typescript
// lib/config.ts
export const GITHUB_CONFIG: GitHubConfig = {
  owner: process.env.NEXT_PUBLIC_GITHUB_OWNER || 'adapatandinnovate',
  repo: process.env.NEXT_PUBLIC_GITHUB_REPO || 'ordx-blog',
  path: process.env.NEXT_PUBLIC_GITHUB_PATH || 'blog',
  branch: process.env.NEXT_PUBLIC_GITHUB_BRANCH || 'main',
  token: process.env.GITHUB_TOKEN,
}

export const SITE_CONFIG = {
  title: 'Discovering Ordinals',
  description: 'All your Ordinals related content in one place!',
  author: 'Ord-X Team',
  siteUrl: process.env.NEXT_PUBLIC_SITE_URL || 'https://ord-x.com',
} as const

export function validateEnvironment(): void {
  const required = [
    'NEXT_PUBLIC_GITHUB_OWNER',
    'NEXT_PUBLIC_GITHUB_REPO',
    'NEXT_PUBLIC_GITHUB_PATH'
  ]
  
  const missing = required.filter(key => !process.env[key])
  if (missing.length > 0) {
    throw new Error(`Missing required environment variables: ${missing.join(', ')}`)
  }
}
```

## Core GitHub API Integration

### Main Blog Functions
```typescript
// lib/blog.ts
import matter from 'gray-matter'
import { remark } from 'remark'
import html from 'remark-html'

async function fetchFromGitHub<T>(endpoint: string): Promise<T> {
  const baseUrl = `https://api.github.com/repos/${GITHUB_CONFIG.owner}/${GITHUB_CONFIG.repo}`
  const headers: HeadersInit = {
    'Accept': 'application/vnd.github.v3+json',
    'User-Agent': 'nextjs-blog-app',
  }
  
  if (GITHUB_CONFIG.token) {
    headers['Authorization'] = `token ${GITHUB_CONFIG.token}`
  }
  
  const response = await fetch(`${baseUrl}${endpoint}`, { 
    headers,
    next: { revalidate: 300 } // ISR: 5 minutes
  })
  
  if (!response.ok) {
    throw new Error(`GitHub API error: ${response.status}`)
  }
  
  return await response.json()
}

export async function getAllBlogSlugs(): Promise<string[]> {
  const files = await fetchDirectoryContents()
  return files.map(file => file.name.replace(/\.md$/, ''))
}

export async function getBlogData(slug: string): Promise<BlogPost> {
  const fileContent = await fetchFileContent(`${slug}.md`)
  const matterResult = matter(fileContent)
  
  // Validate and sanitize frontmatter
  const sanitizedData = sanitizeFrontmatter(matterResult.data, `${slug}.md`)
  
  // Convert markdown to HTML
  const processedContent = await remark()
    .use(html)
    .process(matterResult.content)
  const contentHtml = processedContent.toString()
  
  return {
    slug,
    contentHtml,
    estimatedWordCount: matterResult.content.split(/\s+/).length,
    ...sanitizedData,
  }
}

export async function getAllBlogPosts(): Promise<BlogPostPreview[]> {
  const files = await fetchDirectoryContents()
  
  const allPostsData = await Promise.all(
    files.map(async (file): Promise<BlogPostPreview | null> => {
      try {
        const fileContent = await fetchFileContent(file.name)
        const matterResult = matter(fileContent)
        const sanitizedData = sanitizeFrontmatter(matterResult.data, file.name)
        
        return {
          slug: file.name.replace(/\.md$/, ''),
          ...sanitizedData,
        }
      } catch (error) {
        console.error(`Error processing file ${file.name}:`, error)
        return null
      }
    })
  )
  
  return allPostsData
    .filter((post): post is BlogPostPreview => post !== null)
    .sort((a, b) => new Date(b.date).getTime() - new Date(a.date).getTime())
}
```

## Content Validation System

### Validation Functions
```typescript
// utils/validation.ts
export interface ValidationError {
  field: string
  message: string
  severity: 'error' | 'warning'
}

export function validateFrontmatter(
  frontmatter: Partial<BlogPostFrontmatter>, 
  filename: string
): { isValid: boolean; errors: ValidationError[]; warnings: ValidationError[] } {
  const errors: ValidationError[] = []
  const warnings: ValidationError[] = []

  // Required fields validation
  const requiredFields: (keyof BlogPostFrontmatter)[] = [
    'title', 'description', 'author', 'date', 'category'
  ]

  requiredFields.forEach(field => {
    if (!frontmatter[field]) {
      errors.push({
        field,
        message: `Missing required field: ${field}`,
        severity: 'error'
      })
    }
  })

  // Date validation
  if (frontmatter.date && !isValid(parseISO(frontmatter.date))) {
    errors.push({
      field: 'date',
      message: 'Invalid date format. Use YYYY-MM-DD format',
      severity: 'error'
    })
  }

  // Category validation
  if (frontmatter.category && !isValidCategory(frontmatter.category)) {
    errors.push({
      field: 'category',
      message: `Invalid category. Must be one of: ${BLOG_CONFIG.categories.join(', ')}`,
      severity: 'error'
    })
  }

  return { isValid: errors.length === 0, errors, warnings }
}

export function sanitizeFrontmatter(
  frontmatter: Partial<BlogPostFrontmatter>, 
  filename: string
): BlogPostFrontmatter {
  return {
    title: frontmatter.title || filename.replace('.md', '').replace(/-/g, ' '),
    description: frontmatter.description || 'No description provided',
    author: frontmatter.author || 'Unknown Author',
    date: frontmatter.date || new Date().toISOString().split('T')[0],
    category: isValidCategory(frontmatter.category || '') 
      ? frontmatter.category! 
      : 'Guides',
    readTime: frontmatter.readTime || '5 min read',
    tags: frontmatter.tags?.slice(0, 10) || [],
    heroImage: frontmatter.heroImage || undefined,
    featured: frontmatter.featured || false,
    difficulty: frontmatter.difficulty || 'Beginner',
    // ... other fields with defaults
  }
}
```

## Caching Strategy

### Type-Safe Cache Implementation
```typescript
// utils/cache.ts
class TypedCache<T> {
  private cache = new Map<string, CacheEntry<T>>()
  private stats = { hits: 0, misses: 0 }

  async get<K extends T>(
    type: string, 
    identifier: string, 
    fetchFn: () => Promise<K>
  ): Promise<K> {
    const key = `${type}:${identifier}:${Math.floor(Date.now() / 300000)}` // 5min windows
    
    if (this.cache.has(key)) {
      const entry = this.cache.get(key)!
      if (Date.now() - entry.timestamp < entry.ttl) {
        this.stats.hits++
        return entry.data as K
      }
    }
    
    this.stats.misses++
    const data = await fetchFn()
    
    this.cache.set(key, {
      data,
      timestamp: Date.now(),
      ttl: 5 * 60 * 1000, // 5 minutes
    })
    
    return data
  }
}

export const contentCache = new TypedCache<any>()
```

## Component Architecture

### Server Components (Data Fetching)
```typescript
// app/blog/page.tsx
export default async function BlogPage() {
  const [posts, featuredPost, categories] = await Promise.all([
    getAllBlogPosts(),
    getFeaturedPost(),
    getAllCategories(),
  ])

  return (
    <BlogListing 
      posts={posts} 
      featuredPost={featuredPost} 
      categories={categories}
    />
  )
}
```

### Client Components (Interactivity)
```typescript
// app/blog/BlogListing.tsx
'use client'

interface BlogListingProps {
  posts: BlogPostPreview[]
  featuredPost: BlogPostPreview | null
  categories: (BlogCategory | 'All')[]
}

export default function BlogListing({ posts, featuredPost, categories }: BlogListingProps) {
  const [selectedCategory, setSelectedCategory] = useState<BlogCategory | 'All'>('All')
  const [searchQuery, setSearchQuery] = useState('')
  
  const filteredPosts = useMemo(() => {
    let filtered = posts
    
    if (selectedCategory !== 'All') {
      filtered = filtered.filter(post => post.category === selectedCategory)
    }
    
    if (searchQuery.trim()) {
      const query = searchQuery.toLowerCase()
      filtered = filtered.filter(post => 
        post.title.toLowerCase().includes(query) ||
        post.description.toLowerCase().includes(query)
      )
    }
    
    return filtered
  }, [posts, selectedCategory, searchQuery])

  // Component JSX with TypeScript props
}
```

### Reusable UI Components
```typescript
// app/components/BlogComponents.tsx
interface BlogCardProps {
  post: BlogPostPreview
  showExcerpt?: boolean
}

export function BlogCard({ post, showExcerpt = true }: BlogCardProps) {
  return (
    <Link href={`/blog/${post.slug}`} className="group">
      <article className="bg-white rounded-xl shadow-md overflow-hidden hover:shadow-xl transition-all duration-300">
        {post.heroImage && (
          <div className="relative h-48 w-full overflow-hidden">
            <Image
              src={post.heroImage}
              alt={post.title}
              fill
              className="object-cover group-hover:scale-110 transition-transform duration-300"
              sizes="(max-width: 768px) 100vw, (max-width: 1200px) 50vw, 33vw"
            />
          </div>
        )}
        <div className="p-6">
          <CategoryBadge category={post.category} />
          <h3 className="text-xl font-bold text-gray-900 mb-2 group-hover:text-blue-600 transition-colors">
            {post.title}
          </h3>
          {showExcerpt && (
            <p className="text-gray-600 mb-4 line-clamp-3">
              {post.description}
            </p>
          )}
          {/* Additional content */}
        </div>
      </article>
    </Link>
  )
}
```

## Content Format Specification

### Markdown File Structure
```markdown
---
title: "Bitcoin Ordinals Complete Guide: Everything You Need to Know"
description: "A comprehensive guide to Bitcoin Ordinals covering inscriptions, collections, marketplaces, and investment strategies for 2024."
author: "Sarah Chen"
date: "2024-01-15"
readTime: "12 min read"
category: "Guides"
tags: ["Bitcoin", "Ordinals", "NFT", "Inscriptions"]
heroImage: "https://raw.githubusercontent.com/your-org/ordx-blog-content/main/images/heroes/bitcoin-ordinals-hero.jpg"
featured: true
difficulty: "Intermediate"
seoKeywords: ["bitcoin ordinals", "ordinal inscriptions", "bitcoin nft"]
lastUpdated: "2024-01-20"
tableOfContents: true
newsletter: true
comments: true
socialSharing: true
---

# Introduction

Bitcoin Ordinals represent a groundbreaking development in the Bitcoin ecosystem...

## What Are Bitcoin Ordinals?

Ordinals are a way to inscribe arbitrary data onto individual satoshis...

### Key Features

- **Immutable**: Stored directly on Bitcoin blockchain
- **Unique**: Each ordinal has a unique identifier  
- **Scarce**: Limited by Bitcoin's block space

![Ordinals Explanation](https://raw.githubusercontent.com/your-org/ordx-blog-content/main/images/charts/ordinals-explanation.png)

## How Ordinals Work

The process involves inscribing data directly onto individual satoshis...

[Video: Ordinals Tutorial](https://raw.githubusercontent.com/your-org/ordx-blog-content/main/videos/tutorials/ordinals-tutorial.mp4)

## Conclusion

Bitcoin Ordinals open up new possibilities for digital ownership...
```

### Content Guidelines

#### Required Frontmatter Fields
- `title`: Post title (10-100 characters recommended)
- `description`: SEO description (20-160 characters)
- `author`: Author name
- `date`: Publication date in YYYY-MM-DD format
- `category`: Must match predefined categories

#### Optional Frontmatter Fields
- `readTime`: e.g., "5 min read"
- `tags`: Array of relevant tags (max 10 recommended)
- `heroImage`: Full URL to featured image
- `featured`: Boolean for featured post highlight
- `difficulty`: "Beginner" | "Intermediate" | "Advanced"
- `seoKeywords`: Array for SEO optimization

#### Media Asset Guidelines
- **Images**: Use GitHub raw URLs, optimize for web (WebP preferred)
- **Videos**: MP4 format, max 50MB file size
- **Organization**: Use subfolder structure (heroes/, screenshots/, charts/)

## Advanced Features

### Search Functionality
```typescript
// utils/search.ts
export function searchPosts(
  query: string, 
  searchIndex: SearchIndex[], 
  options: SearchOptions = {}
): SearchResult[] {
  const terms = query.toLowerCase().split(' ').filter(term => term.length > 1)
  
  return searchIndex
    .map(post => {
      let score = 0
      
      terms.forEach(term => {
        if (post.title.toLowerCase().includes(term)) score += 3
        if (post.description.toLowerCase().includes(term)) score += 2
        if (post.tags.some(tag => tag.toLowerCase().includes(term))) score += 2
        if (post.category.toLowerCase().includes(term)) score += 1
      })
      
      return { ...post, score }
    })
    .filter(post => post.score > 0)
    .sort((a, b) => b.score - a.score)
}
```

### Performance Monitoring
```typescript
// utils/performance.ts
export class BuildPerformanceTracker {
  private metrics = {
    totalBuildTime: 0,
    apiCalls: 0,
    cacheHits: 0,
    cacheMisses: 0,
    postsProcessed: 0,
    errors: 0,
  }

  trackApiCall(): void { this.metrics.apiCalls++ }
  trackCacheHit(): void { this.metrics.cacheHits++ }
  trackError(): void { this.metrics.errors++ }
  
  report(): void {
    const cacheHitRate = this.metrics.cacheHits / (this.metrics.cacheHits + this.metrics.cacheMisses) * 100
    console.log(`📊 Performance: ${cacheHitRate.toFixed(1)}% cache hit rate`)
  }
}
```

## Build and Deployment Configuration

### Package.json Dependencies
```json
{
  "dependencies": {
    "next": "14.0.0",
    "react": "^18",
    "react-dom": "^18",
    "gray-matter": "^4.0.3",
    "remark": "^15.0.1",
    "remark-html": "^16.0.1",
    "date-fns": "^2.30.0"
  },
  "devDependencies": {
    "@types/node": "^20",
    "@types/react": "^18",
    "@types/react-dom": "^18",
    "typescript": "^5",
    "tailwindcss": "^3.3.0",
    "@tailwindcss/typography": "^0.5.10"
  },
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "type-check": "tsc --noEmit"
  }
}
```

### TypeScript Configuration
```json
{
  "compilerOptions": {
    "target": "es5",
    "lib": ["dom", "dom.iterable", "es6"],
    "allowJs": true,
    "skipLibCheck": true,
    "strict": true,
    "noEmit": true,
    "esModuleInterop": true,
    "module": "esnext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,
    "plugins": [{ "name": "next" }],
    "baseUrl": ".",
    "paths": {
      "@/*": ["./*"],
      "@/components/*": ["./app/components/*"],
      "@/lib/*": ["./lib/*"],
      "@/types/*": ["./types/*"],
      "@/utils/*": ["./utils/*"]
    }
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"],
  "exclude": ["node_modules"]
}
```

### Next.js Configuration
```javascript
/** @type {import('next').NextConfig} */
const nextConfig = {
  typescript: {
    ignoreBuildErrors: false,
  },
  experimental: {
    typedRoutes: true,
  },
  images: {
    remotePatterns: [
      {
        protocol: 'https',
        hostname: '*.githubusercontent.com',
        pathname: '/**',
      },
    ],
  },
  async headers() {
    return [
      {
        source: '/blog/:path*',
        headers: [
          {
            key: 'Cache-Control',
            value: 'public, max-age=3600, stale-while-revalidate=86400',
          },
        ],
      },
    ]
  },
}

module.exports = nextConfig
```

### Tailwind Configuration
```typescript
import type { Config } from 'tailwindcss'

const config: Config = {
  content: [
    './pages/**/*.{js,ts,jsx,tsx,mdx}',
    './components/**/*.{js,ts,jsx,tsx,mdx}',
    './app/**/*.{js,ts,jsx,tsx,mdx}',
  ],
  theme: {
    extend: {
      typography: {
        DEFAULT: {
          css: {
            maxWidth: 'none',
          },
        },
      },
    },
  },
  plugins: [
    require('@tailwindcss/typography'),
    require('@tailwindcss/line-clamp'),
  ],
}

export default config
```

## Development Workflow

### Setup Process
1. **Repository Creation**: Create main app repository with TypeScript setup
2. **Environment Setup**: Configure GitHub API credentials and repository settings
3. **Content Repository**: Create separate repository for markdown content and media
4. **Build Pipeline**: Implement GitHub API integration with caching and validation
5. **Component Development**: Build type-safe React components with proper interfaces
6. **Testing**: Implement content validation and error handling
7. **Deployment**: Configure ISR and performance optimization

### Content Management Process
1. **Content Creation**: Writers add markdown files to content repository
2. **Media Management**: Upload images/videos to organized folder structure
3. **Validation**: Automatic frontmatter validation on commit
4. **Publishing**: Git push triggers webhook for automatic deployment
5. **Monitoring**: Performance tracking and error reporting

### Team Responsibilities

#### Developers
- Maintain main application repository
- Implement new UI components and features
- Handle build configuration and deployment
- Monitor performance and error tracking

#### Content Team
- Manage content repository independently
- Write articles following markdown specification
- Upload and organize media assets
- Follow content guidelines and validation rules

## Error Handling and Troubleshooting

### Common Issues and Solutions

#### Build Failures
- **GitHub API Rate Limits**: Add GITHUB_TOKEN environment variable
- **Missing Environment Variables**: Verify all required env vars are set
- **Invalid Frontmatter**: Check validation errors in build logs
- **Image Loading Issues**: Ensure Next.js image domains are configured

#### TypeScript Errors
- **Type Mismatches**: Verify interfaces match actual data structure
- **Missing Properties**: Add optional properties or provide defaults
- **Import Errors**: Check path aliases and module resolution

#### Performance Issues
- **Slow Builds**: Implement caching and optimize API calls
- **Large Bundle Size**: Use dynamic imports and code splitting
- **Memory Issues**: Optimize image processing and content parsing

### Debug Strategies
1. **Enable Verbose Logging**: Add detailed console.log statements
2. **Type Checking**: Use `npm run type-check` to catch type errors
3. **Content Validation**: Test with sample content before production
4. **Performance Monitoring**: Track build metrics and API response times

## Deployment Instructions

### Vercel Deployment
1. **Connect Repository**: Link main app repository to Vercel
2. **Environment Variables**: Add all required env vars in Vercel dashboard
3. **Build Settings**: Configure build command and output directory
4. **Domain Setup**: Configure custom domain and SSL

### Alternative Platforms
- **Netlify**: Similar setup with build environment configuration
- **Railway**: Database integration if needed for future features
- **DigitalOcean**: App Platform with container deployment

## Security Considerations

### API Security
- **Rate Limiting**: Implement caching to reduce API calls
- **Token Security**: Use environment variables for sensitive data
- **CORS Configuration**: Restrict API access to authorized domains

### Content Security
- **Input Validation**: Sanitize all frontmatter data
- **XSS Prevention**: Use dangerouslySetInnerHTML carefully
- **Image Optimization**: Validate image URLs and implement CSP

This documentation provides complete implementation details for recreating the TypeScript blog system with separate GitHub content repository. The system maintains strict separation between application code and content while providing full type safety and production-ready features.

## Testing Strategy

### Unit Testing Setup
```typescript
// tests/setup.ts
import { beforeEach, afterEach } from '@jest/globals'

// Mock GitHub API for consistent testing
global.fetch = jest.fn()

beforeEach(() => {
  fetch.mockClear()
})

// Mock data for testing
export const mockBlogPost = {
  name: 'test-post.md',
  content: Buffer.from(`---
title: "Test Post"
description: "A test blog post"
author: "Test Author"
date: "2024-01-15"
category: "Guides"
---

# Test Content

This is a test post.`).toString('base64'),
  encoding: 'base64'
}

export const mockDirectoryListing = [
  { name: 'test-post.md', type: 'file' },
  { name: 'another-post.md', type: 'file' }
]
```

### Content Validation Tests
```typescript
// tests/validation.test.ts
import { validateFrontmatter, sanitizeFrontmatter } from '@/utils/validation'

describe('Content Validation', () => {
  test('validates required frontmatter fields', () => {
    const frontmatter = {
      title: 'Test Post',
      description: 'Test description',
      author: 'Test Author',
      date: '2024-01-15',
      category: 'Guides' as BlogCategory
    }
    
    const result = validateFrontmatter(frontmatter, 'test.md')
    expect(result.isValid).toBe(true)
    expect(result.errors).toHaveLength(0)
  })
  
  test('catches missing required fields', () => {
    const frontmatter = { title: 'Test Post' }
    const result = validateFrontmatter(frontmatter, 'test.md')
    
    expect(result.isValid).toBe(false)
    expect(result.errors.some(e => e.field === 'description')).toBe(true)
  })
  
  test('sanitizes invalid data with defaults', () => {
    const frontmatter = { title: 'Test Post' }
    const sanitized = sanitizeFrontmatter(frontmatter, 'test-post.md')
    
    expect(sanitized.description).toBe('No description provided')
    expect(sanitized.category).toBe('Guides')
    expect(sanitized.author).toBe('Unknown Author')
  })
})
```

## Advanced Component Patterns

### Generic Hook for Content Operations
```typescript
// hooks/useContent.ts
import { useState, useEffect } from 'react'

export function useContent<T>(
  fetchFn: () => Promise<T>,
  dependencies: any[] = []
) {
  const [data, setData] = useState<T | null>(null)
  const [loading, setLoading] = useState(true)
  const [error, setError] = useState<string | null>(null)

  useEffect(() => {
    let isMounted = true

    const fetchData = async () => {
      try {
        setLoading(true)
        setError(null)
        const result = await fetchFn()
        
        if (isMounted) {
          setData(result)
        }
      } catch (err) {
        if (isMounted) {
          setError(err instanceof Error ? err.message : 'Unknown error')
        }
      } finally {
        if (isMounted) {
          setLoading(false)
        }
      }
    }

    fetchData()

    return () => {
      isMounted = false
    }
  }, dependencies)

  return { data, loading, error, refetch: () => fetchData() }
}

// Usage example
function BlogPostList() {
  const { data: posts, loading, error } = useContent(getAllBlogPosts)
  
  if (loading) return <LoadingSpinner />
  if (error) return <ErrorMessage error={error} />
  if (!posts) return <EmptyState />
  
  return (
    <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      {posts.map(post => <BlogCard key={post.slug} post={post} />)}
    </div>
  )
}
```

### Higher-Order Component for Error Boundaries
```typescript
// components/withErrorBoundary.tsx
import React, { Component, ErrorInfo, ReactNode } from 'react'

interface Props {
  children: ReactNode
  fallback?: ReactNode
  onError?: (error: Error, errorInfo: ErrorInfo) => void
}

interface State {
  hasError: boolean
  error?: Error
}

class ErrorBoundary extends Component<Props, State> {
  constructor(props: Props) {
    super(props)
    this.state = { hasError: false }
  }

  static getDerivedStateFromError(error: Error): State {
    return { hasError: true, error }
  }

  componentDidCatch(error: Error, errorInfo: ErrorInfo) {
    console.error('Error caught by boundary:', error, errorInfo)
    this.props.onError?.(error, errorInfo)
  }

  render() {
    if (this.state.hasError) {
      return this.props.fallback || (
        <div className="p-6 text-center">
          <h2 className="text-xl font-semibold text-red-600 mb-2">
            Something went wrong
          </h2>
          <p className="text-gray-600">
            {this.state.error?.message || 'An unexpected error occurred'}
          </p>
        </div>
      )
    }

    return this.props.children
  }
}

export function withErrorBoundary<P extends object>(
  Component: React.ComponentType<P>,
  fallback?: ReactNode
) {
  return function WrappedComponent(props: P) {
    return (
      <ErrorBoundary fallback={fallback}>
        <Component {...props} />
      </ErrorBoundary>
    )
  }
}
```

## API Route Extensions

### Search API Endpoint
```typescript
// app/api/search/route.ts
import { NextRequest, NextResponse } from 'next/server'
import { getAllBlogPosts } from '@/lib/blog'
import { createSearchIndex, searchPosts } from '@/utils/search'

export async function GET(request: NextRequest) {
  try {
    const searchParams = request.nextUrl.searchParams
    const query = searchParams.get('q')
    const limit = parseInt(searchParams.get('limit') || '10')
    const category = searchParams.get('category')

    if (!query || query.length < 2) {
      return NextResponse.json({ error: 'Query must be at least 2 characters' }, { status: 400 })
    }

    const posts = await getAllBlogPosts()
    let filteredPosts = posts

    if (category && category !== 'All') {
      filteredPosts = posts.filter(post => post.category === category)
    }

    const searchIndex = createSearchIndex(filteredPosts)
    const results = searchPosts(query, searchIndex, {
      fuzzySearch: true,
      titleWeight: 3,
      descriptionWeight: 2,
      tagWeight: 2
    }).slice(0, limit)

    return NextResponse.json({
      query,
      results,
      total: results.length,
      category: category || 'All'
    })

  } catch (error) {
    console.error('Search API error:', error)
    return NextResponse.json(
      { error: 'Internal server error' }, 
      { status: 500 }
    )
  }
}
```

### Analytics API Endpoint
```typescript
// app/api/analytics/route.ts
import { NextRequest, NextResponse } from 'next/server'

interface AnalyticsEvent {
  event: string
  properties: Record<string, any>
  timestamp?: number
}

export async function POST(request: NextRequest) {
  try {
    const { event, properties }: AnalyticsEvent = await request.json()

    // Validate event data
    if (!event || typeof event !== 'string') {
      return NextResponse.json({ error: 'Invalid event name' }, { status: 400 })
    }

    // Log event (in production, send to analytics service)
    console.log('Analytics Event:', {
      event,
      properties,
      timestamp: Date.now(),
      userAgent: request.headers.get('user-agent'),
      ip: request.ip || 'unknown'
    })

    // In production, integrate with your analytics service:
    // - Google Analytics 4
    // - Mixpanel
    // - PostHog
    // - Custom analytics database

    return NextResponse.json({ success: true })

  } catch (error) {
    console.error('Analytics API error:', error)
    return NextResponse.json(
      { error: 'Failed to track event' }, 
      { status: 500 }
    )
  }
}
```

## Content Management Automation

### GitHub Actions Workflow for Content Repository
```yaml
# .github/workflows/validate-content.yml (in content repository)
name: Validate Blog Content

on:
  push:
    branches: [main]
    paths: ['blog/**/*.md']
  pull_request:
    branches: [main]
    paths: ['blog/**/*.md']

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
          
      - name: Install dependencies for validation
        run: |
          npm init -y
          npm install gray-matter js-yaml date-fns
      
      - name: Validate Markdown Files
        run: |
          node -e "
          const fs = require('fs');
          const path = require('path');
          const matter = require('gray-matter');
          const { parseISO, isValid } = require('date-fns');
          
          const blogDir = path.join(process.cwd(), 'blog');
          const files = fs.readdirSync(blogDir).filter(f => f.endsWith('.md'));
          
          let hasErrors = false;
          
          files.forEach(file => {
            try {
              const content = fs.readFileSync(path.join(blogDir, file), 'utf8');
              const { data } = matter(content);
              
              // Validate required fields
              const required = ['title', 'description', 'author', 'date', 'category'];
              const missing = required.filter(field => !data[field]);
              
              if (missing.length > 0) {
                console.error(\`❌ \${file}: Missing required fields: \${missing.join(', ')}\`);
                hasErrors = true;
              }
              
              // Validate date format
              if (data.date && !isValid(parseISO(data.date))) {
                console.error(\`❌ \${file}: Invalid date format: \${data.date}\`);
                hasErrors = true;
              }
              
              // Validate category
              const validCategories = ['Guides', 'News', 'Tools', 'Analysis', 'Getting Started', 'Tutorial'];
              if (data.category && !validCategories.includes(data.category)) {
                console.error(\`❌ \${file}: Invalid category: \${data.category}\`);
                hasErrors = true;
              }
              
              console.log(\`✅ \${file}: Valid\`);
              
            } catch (error) {
              console.error(\`❌ \${file}: Parse error - \${error.message}\`);
              hasErrors = true;
            }
          });
          
          if (hasErrors) {
            process.exit(1);
          } else {
            console.log('🎉 All content files are valid!');
          }
          "
      
      - name: Notify Main App Repository
        if: github.ref == 'refs/heads/main'
        uses: peter-evans/repository-dispatch@v2
        with:
          token: ${{ secrets.REPO_ACCESS_TOKEN }}
          repository: your-org/your-nextjs-app
          event-type: content-updated
          client-payload: |
            {
              "ref": "${{ github.ref }}",
              "sha": "${{ github.sha }}",
              "modified_files": "${{ toJson(github.event.commits[0].modified) }}"
            }
```

### Content Repository Webhook Handler
```typescript
// app/api/webhook/content-updated/route.ts
import { NextRequest, NextResponse } from 'next/server'
import { revalidateTag } from 'next/cache'
import crypto from 'crypto'

export async function POST(request: NextRequest) {
  try {
    // Verify webhook signature
    const signature = request.headers.get('x-hub-signature-256')
    const body = await request.text()
    
    if (signature && process.env.WEBHOOK_SECRET) {
      const expectedSignature = 'sha256=' + 
        crypto.createHmac('sha256', process.env.WEBHOOK_SECRET)
              .update(body)
              .digest('hex')
      
      if (signature !== expectedSignature) {
        return NextResponse.json({ error: 'Invalid signature' }, { status: 401 })
      }
    }

    const payload = JSON.parse(body)
    
    // Log the update
    console.log('Content updated:', {
      ref: payload.ref,
      sha: payload.sha?.substring(0, 7),
      modifiedFiles: payload.modified_files?.length || 0
    })

    // Invalidate relevant caches
    revalidateTag('blog-posts')
    revalidateTag('featured-post')
    revalidateTag('categories')

    // Trigger rebuild if using external deployment service
    if (process.env.VERCEL_HOOK_URL) {
      await fetch(process.env.VERCEL_HOOK_URL, { method: 'POST' })
    }

    return NextResponse.json({ 
      message: 'Content updated successfully',
      revalidated: true,
      timestamp: new Date().toISOString()
    })

  } catch (error) {
    console.error('Webhook error:', error)
    return NextResponse.json(
      { error: 'Webhook processing failed' }, 
      { status: 500 }
    )
  }
}
```

## SEO and Performance Optimization

### Dynamic Sitemap Generation
```typescript
// app/sitemap.ts
import { MetadataRoute } from 'next'
import { getAllBlogPosts } from '@/lib/blog'
import { SITE_CONFIG } from '@/lib/config'

export default async function sitemap(): Promise<MetadataRoute.Sitemap> {
  const posts = await getAllBlogPosts()
  
  const blogUrls: MetadataRoute.Sitemap = posts.map((post) => ({
    url: `${SITE_CONFIG.siteUrl}/blog/${post.slug}`,
    lastModified: post.lastUpdated || post.date,
    changeFrequency: 'weekly',
    priority: post.featured ? 0.9 : 0.7,
  }))

  return [
    {
      url: SITE_CONFIG.siteUrl,
      lastModified: new Date(),
      changeFrequency: 'daily',
      priority: 1,
    },
    {
      url: `${SITE_CONFIG.siteUrl}/blog`,
      lastModified: new Date(),
      changeFrequency: 'daily',
      priority: 0.8,
    },
    ...blogUrls,
  ]
}
```

### Structured Data for SEO
```typescript
// components/StructuredData.tsx
import { BlogPost } from '@/types/blog'
import { SITE_CONFIG } from '@/lib/config'

interface StructuredDataProps {
  post: BlogPost
}

export function StructuredData({ post }: StructuredDataProps) {
  const structuredData = {
    '@context': 'https://schema.org',
    '@type': 'BlogPosting',
    headline: post.title,
    description: post.description,
    image: post.heroImage ? [post.heroImage] : [],
    datePublished: post.date,
    dateModified: post.lastUpdated || post.date,
    author: {
      '@type': 'Person',
      name: post.author,
    },
    publisher: {
      '@type': 'Organization',
      name: SITE_CONFIG.author,
      logo: {
        '@type': 'ImageObject',
        url: `${SITE_CONFIG.siteUrl}/logo.png`,
      },
    },
    mainEntityOfPage: {
      '@type': 'WebPage',
      '@id': `${SITE_CONFIG.siteUrl}/blog/${post.slug}`,
    },
    keywords: post.seoKeywords?.join(', '),
    wordCount: post.estimatedWordCount,
    genre: post.category,
    learningResourceType: post.difficulty,
  }

  return (
    <script
      type="application/ld+json"
      dangerouslySetInnerHTML={{
        __html: JSON.stringify(structuredData, null, 2),
      }}
    />
  )
}
```

## Monitoring and Analytics

### Performance Monitoring Hook
```typescript
// hooks/usePerformanceMonitoring.ts
import { useEffect } from 'react'

interface PerformanceMetrics {
  pageLoadTime?: number
  firstContentfulPaint?: number
  largestContentfulPaint?: number
  cumulativeLayoutShift?: number
  firstInputDelay?: number
}

export function usePerformanceMonitoring(pageName: string) {
  useEffect(() => {
    const observer = new PerformanceObserver((list) => {
      const metrics: PerformanceMetrics = {}
      
      for (const entry of list.getEntries()) {
        switch (entry.name) {
          case 'first-contentful-paint':
            metrics.firstContentfulPaint = entry.startTime
            break
          case 'largest-contentful-paint':
            metrics.largestContentfulPaint = entry.startTime
            break
        }
      }
      
      // Send metrics to analytics
      if (Object.keys(metrics).length > 0) {
        fetch('/api/analytics', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({
            event: 'performance_metrics',
            properties: {
              page: pageName,
              ...metrics,
              timestamp: Date.now()
            }
          })
        }).catch(() => {}) // Silent fail
      }
    })
    
    observer.observe({ entryTypes: ['paint', 'largest-contentful-paint'] })
    
    return () => observer.disconnect()
  }, [pageName])
}
```

### Error Tracking Service Integration
```typescript
// lib/errorTracking.ts
interface ErrorContext {
  component?: string
  action?: string
  userId?: string
  metadata?: Record<string, any>
}

export class ErrorTracker {
  static capture(error: Error, context: ErrorContext = {}) {
    // Log locally
    console.error('Error captured:', error, context)
    
    // In production, integrate with error tracking service:
    // - Sentry
    // - Bugsnag
    // - LogRocket
    // - Custom error service
    
    const errorData = {
      message: error.message,
      stack: error.stack,
      timestamp: new Date().toISOString(),
      url: window.location.href,
      userAgent: navigator.userAgent,
      ...context
    }
    
    // Send to error tracking service
    fetch('/api/errors', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(errorData)
    }).catch(() => {}) // Silent fail to prevent error loops
  }
  
  static captureMessage(message: string, level: 'info' | 'warning' | 'error' = 'info') {
    console.log(`[${level.toUpperCase()}] ${message}`)
    
    fetch('/api/logs', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        level,
        message,
        timestamp: new Date().toISOString(),
        url: window.location.href
      })
    }).catch(() => {})
  }
}

// Usage in components
export function withErrorTracking<P extends object>(
  Component: React.ComponentType<P>,
  componentName: string
) {
  return function TrackedComponent(props: P) {
    useEffect(() => {
      const handleError = (event: ErrorEvent) => {
        ErrorTracker.capture(new Error(event.message), {
          component: componentName,
          action: 'runtime_error'
        })
      }
      
      window.addEventListener('error', handleError)
      return () => window.removeEventListener('error', handleError)
    }, [])
    
    return <Component {...props} />
  }
}
```

## Production Checklist

### Pre-Deployment Verification
```typescript
// scripts/pre-deploy-check.ts
import { getAllBlogPosts, getBlogData } from '@/lib/blog'
import { validateEnvironment } from '@/lib/config'

async function runPreDeploymentChecks() {
  console.log('🔍 Running pre-deployment checks...')
  
  try {
    // Environment validation
    console.log('✅ Validating environment variables...')
    validateEnvironment()
    
    // Content accessibility check
    console.log('✅ Checking content repository access...')
    const posts = await getAllBlogPosts()
    console.log(`📚 Found ${posts.length} blog posts`)
    
    // Sample content validation
    console.log('✅ Validating sample content...')
    if (posts.length > 0) {
      const samplePost = await getBlogData(posts[0].slug)
      if (!samplePost.contentHtml) {
        throw new Error('Content processing failed')
      }
    }
    
    // Performance check
    console.log('✅ Running performance check...')
    const startTime = Date.now()
    await getAllBlogPosts()
    const duration = Date.now() - startTime
    console.log(`⚡ Content fetching took ${duration}ms`)
    
    if (duration > 5000) {
      console.warn('⚠️  Content fetching is slow, consider adding GitHub token')
    }
    
    console.log('🎉 All pre-deployment checks passed!')
    
  } catch (error) {
    console.error('❌ Pre-deployment check failed:', error)
    process.exit(1)
  }
}

runPreDeploymentChecks()
```

### Health Check Endpoint
```typescript
// app/api/health/route.ts
import { NextResponse } from 'next/server'
import { getAllBlogPosts } from '@/lib/blog'

export async function GET() {
  try {
    const startTime = Date.now()
    
    // Check GitHub API connectivity
    const posts = await getAllBlogPosts()
    const duration = Date.now() - startTime
    
    // Check if we have content
    if (posts.length === 0) {
      return NextResponse.json({
        status: 'warning',
        message: 'No content found',
        timestamp: new Date().toISOString()
      }, { status: 200 })
    }
    
    return NextResponse.json({
      status: 'healthy',
      data: {
        totalPosts: posts.length,
        lastUpdate: posts[0]?.date,
        responseTime: `${duration}ms`
      },
      timestamp: new Date().toISOString()
    })
    
  } catch (error) {
    return NextResponse.json({
      status: 'error',
      error: error instanceof Error ? error.message : 'Unknown error',
      timestamp: new Date().toISOString()
    }, { status: 500 })
  }
}
```

This comprehensive documentation provides Claude Code with everything needed to recreate a production-ready TypeScript blog system with complete separation between application code and content management. The system includes advanced features like testing, monitoring, SEO optimization, and deployment automation while maintaining strict type safety throughout.