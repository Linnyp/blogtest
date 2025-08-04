# Ordx Blog Content Repository

This repository contains all blog content for the Ordx blog system, including markdown articles, images, videos, and other media assets.

## Repository Structure

```
ordx-blog-content/
├── blog/                     # Markdown articles
├── images/                   # Image assets organized by type
│   ├── heroes/              # Large featured images
│   ├── screenshots/         # UI screenshots
│   ├── charts/              # Data visualizations
│   └── misc/                # Other images
├── videos/                   # Video content
│   ├── tutorials/           # Tutorial videos
│   └── animations/          # Animated content
├── docs/                    # Content guidelines
│   ├── writing-style-guide.md
│   └── markdown-template.md
├── .gitignore               # Git ignore rules
└── README.md                # This file
```

## Content Guidelines

### Writing Articles

1. Use the markdown template in `docs/markdown-template.md`
2. Follow the style guide in `docs/writing-style-guide.md`
3. Ensure all required frontmatter fields are included
4. Use descriptive filenames in kebab-case

### Media Assets

#### Images
- **Heroes**: 1200x630px, under 200KB, WebP/JPG format
- **Screenshots**: Actual resolution, under 500KB, PNG/JPG format
- **Charts**: SVG preferred for scalability, under 300KB
- **Misc**: Optimized for intended use, under 200KB

#### Videos
- **Format**: MP4 (H.264 codec)
- **Resolution**: 1080p or 720p
- **Size**: Under 50MB per video
- **Naming**: descriptive-kebab-case.mp4

### Frontmatter Requirements

#### Required Fields
```yaml
title: "Article Title"
description: "SEO description (20-160 chars)"
author: "Author Name"
date: "YYYY-MM-DD"
category: "One of: Guides|News|Tools|Analysis|Getting Started|Tutorial"
```

#### Optional Fields
```yaml
readTime: "X min read"
tags: ["tag1", "tag2"]
heroImage: "https://raw.githubusercontent.com/.../image.jpg"
featured: true|false
difficulty: "Beginner|Intermediate|Advanced"
seoKeywords: ["keyword1", "keyword2"]
lastUpdated: "YYYY-MM-DD"
tableOfContents: true|false
newsletter: true|false
comments: true|false
socialSharing: true|false
```

## Workflow

### Adding New Content

1. Create markdown file in `blog/` directory
2. Add media assets to appropriate folders
3. Use full GitHub raw URLs for media references
4. Test content with validation tools
5. Submit pull request for review

### Content Review Process

1. Automated validation runs on PR creation
2. Manual review for content quality and accuracy
3. Merge after approval
4. Automatic deployment trigger to main blog

### Media Organization

- Use descriptive, SEO-friendly filenames
- Organize by content type in appropriate folders
- Optimize file sizes for web delivery
- Use GitHub raw URLs in markdown content

## Content Validation

The repository includes automated validation for:
- Required frontmatter fields
- Date format validation
- Category validation
- File size limits
- Image format compliance

## Integration

This content repository integrates with the main blog application via:
- GitHub API for content fetching
- Automated webhooks for content updates
- ISR (Incremental Static Regeneration) for performance
- CDN caching for media assets

## Support

For questions about content creation or repository structure:
1. Review the documentation in `docs/`
2. Check existing content for examples
3. Contact the development team for technical issues
4. Submit issues for content guidelines clarification

## License

Content in this repository is proprietary. See LICENSE file for details.