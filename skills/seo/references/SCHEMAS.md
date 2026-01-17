# LD+JSON Schema Templates

Copy and customize these templates for your content.

## Article (Blog Posts)

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "Your Article Title",
  "description": "Brief description of the article",
  "image": "https://adynato.com/images/blog/post-slug/cover.png",
  "datePublished": "2026-01-17T00:00:00Z",
  "dateModified": "2026-01-17T00:00:00Z",
  "author": {
    "@type": "Person",
    "name": "Author Name",
    "url": "https://adynato.com/team/author"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Adynato",
    "logo": {
      "@type": "ImageObject",
      "url": "https://adynato.com/logo.png"
    }
  },
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://adynato.com/blog/post-slug"
  }
}
```

## TechArticle (Documentation)

```json
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "headline": "Documentation Title",
  "description": "What this documentation covers",
  "datePublished": "2026-01-17T00:00:00Z",
  "dateModified": "2026-01-17T00:00:00Z",
  "author": {
    "@type": "Organization",
    "name": "Adynato"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Adynato"
  },
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://adynato.com/docs/page"
  },
  "proficiencyLevel": "Beginner"
}
```

## BreadcrumbList

```json
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    {
      "@type": "ListItem",
      "position": 1,
      "name": "Home",
      "item": "https://adynato.com"
    },
    {
      "@type": "ListItem",
      "position": 2,
      "name": "Blog",
      "item": "https://adynato.com/blog"
    },
    {
      "@type": "ListItem",
      "position": 3,
      "name": "Post Title",
      "item": "https://adynato.com/blog/post-slug"
    }
  ]
}
```

## Organization

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Adynato",
  "url": "https://adynato.com",
  "logo": "https://adynato.com/logo.png",
  "sameAs": [
    "https://github.com/adynato",
    "https://twitter.com/adynato"
  ],
  "contactPoint": {
    "@type": "ContactPoint",
    "contactType": "customer support",
    "url": "https://adynato.com/contact"
  }
}
```

## WebPage (Landing Pages)

```json
{
  "@context": "https://schema.org",
  "@type": "WebPage",
  "name": "Page Title",
  "description": "Page description",
  "url": "https://adynato.com/page",
  "isPartOf": {
    "@type": "WebSite",
    "name": "Adynato",
    "url": "https://adynato.com"
  }
}
```

## Product

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Product Name",
  "description": "Product description",
  "image": "https://adynato.com/images/product.png",
  "brand": {
    "@type": "Organization",
    "name": "Adynato"
  },
  "offers": {
    "@type": "Offer",
    "price": "0",
    "priceCurrency": "USD",
    "availability": "https://schema.org/InStock"
  }
}
```

## SoftwareApplication

```json
{
  "@context": "https://schema.org",
  "@type": "SoftwareApplication",
  "name": "App Name",
  "description": "What the app does",
  "applicationCategory": "DeveloperApplication",
  "operatingSystem": "Any",
  "offers": {
    "@type": "Offer",
    "price": "0",
    "priceCurrency": "USD"
  },
  "author": {
    "@type": "Organization",
    "name": "Adynato"
  }
}
```

## Combined Graph Example

For a blog post, combine Article, BreadcrumbList, and Organization:

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Article",
      "headline": "How to Optimize Images for Web",
      "description": "Learn how to use img4web to optimize images",
      "image": "https://adynato.com/images/blog/optimize-images/cover.png",
      "datePublished": "2026-01-17T00:00:00Z",
      "dateModified": "2026-01-17T00:00:00Z",
      "author": {
        "@type": "Person",
        "name": "Adar"
      },
      "publisher": {
        "@id": "#organization"
      },
      "mainEntityOfPage": {
        "@type": "WebPage",
        "@id": "https://adynato.com/blog/optimize-images"
      }
    },
    {
      "@type": "BreadcrumbList",
      "itemListElement": [
        {
          "@type": "ListItem",
          "position": 1,
          "name": "Home",
          "item": "https://adynato.com"
        },
        {
          "@type": "ListItem",
          "position": 2,
          "name": "Blog",
          "item": "https://adynato.com/blog"
        },
        {
          "@type": "ListItem",
          "position": 3,
          "name": "How to Optimize Images for Web",
          "item": "https://adynato.com/blog/optimize-images"
        }
      ]
    },
    {
      "@type": "Organization",
      "@id": "#organization",
      "name": "Adynato",
      "url": "https://adynato.com",
      "logo": "https://adynato.com/logo.png"
    }
  ]
}
```
