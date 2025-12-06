# Motif — Client Review Grid Component

## Overview
Motif is a sophisticated client testimonial grid component featuring a structured two-column layout with integrated company branding and user profiles. Designed for showcasing professional reviews with visual hierarchy and responsive design.

## Live Preview
[View Live Demo](https://thisislefa.github.io/Motif) | [GitHub Repository](https://github.com/thisislefa/motif)

## Technical Architecture

### Core Features
- **Responsive Grid Layout**: 2-column desktop, 1-column mobile with adaptive spacing
- **Semantic HTML Structure**: Proper use of article, header, and section elements
- **Performance Optimized**: Minimal CSS with efficient selector patterns
- **Accessibility First**: ARIA labels, keyboard navigation, screen reader support
- **No Dependencies**: Pure HTML/CSS with optional JavaScript enhancements

### Design System
```css
:root {
    /* Color Palette */
    --color-bg: #ffffff;
    --color-card-bg: #F9FAFB;
    --color-text-primary: #111827;
    --color-text-secondary: #6B7280;
    --color-text-tertiary: #4B5563;
    --color-border: #E5E7EB;
    --color-accent: #000000;
    --color-star-filled: #000000;
    --color-star-empty: #D1D5DB;
    
    /* Typography */
    --font-family: 'Inter', sans-serif;
    --font-size-title: 48px;
    --font-size-review: 18px;
    --font-size-meta: 15px;
    
    /* Spacing */
    --spacing-card: 32px;
    --spacing-grid: 24px;
    --spacing-section: 40px;
    
    /* Borders */
    --border-radius: 12px;
    --border-width: 1px;
    
    /* Transitions */
    --transition-speed: 0.2s;
    --transition-timing: ease;
}
```

### Grid System
```css
/* Mobile-first responsive grid */
.cr-reviews-grid {
    display: grid;
    gap: var(--spacing-grid);
    grid-template-columns: 1fr;
}

@media (min-width: 900px) {
    .cr-reviews-grid {
        grid-template-columns: repeat(2, 1fr);
    }
}

/* Card internal grid for profile + content */
.cr-card-body {
    display: grid;
    gap: 20px;
    grid-template-columns: 150px 1fr;
}

@media (max-width: 900px) {
    .cr-card-body {
        grid-template-columns: 1fr;
    }
}
```

## Installation & Usage

### Direct Implementation
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/thisislefa/motif@latest/dist/motif.css">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body>
    <motif-reviews 
        title="Client Reviews"
        cta-text="Get Template"
        cta-url="/templates"
        :reviews="reviews"
    ></motif-reviews>
    
    <script src="https://cdn.jsdelivr.net/gh/thisislefa/motif@latest/dist/motif.js" type="module"></script>
</body>
</html>
```

### NPM Package
```bash
npm install @thisislefa/motif
```

### Web Component Usage
```javascript
import '@thisislefa/motif';

// Register custom element
customElements.define('motif-reviews', MotifReviews);
```

## Framework Integration

### React Component
```jsx
import React from 'react';
import Motif from '@thisislefa/motif/react';
import '@thisislefa/motif/dist/motif.css';

function ReviewSection() {
    const reviews = [
        {
            id: 1,
            company: {
                name: 'Designnest',
                icon: 'fa-border-all',
                color: '#4F46E5'
            },
            rating: 5,
            author: {
                name: 'Emily Davis',
                role: 'Founder, Designnest',
                avatar: 'https://example.com/avatar.jpg'
            },
            content: 'The designs were nothing short of spectacular...',
            date: '2024-03-15',
            verified: true
        }
    ];

    return (
        <Motif 
            title="Client Reviews"
            ctaText="Get Template"
            ctaUrl="/templates"
            reviews={reviews}
            onReviewClick={(review) => console.log('Review clicked:', review)}
            theme="light"
        />
    );
}
```

### Vue 3 Component
```vue
<template>
    <motif-reviews
        :title="title"
        :cta-text="ctaText"
        :cta-url="ctaUrl"
        :reviews="reviews"
        @review-click="handleReviewClick"
    />
</template>

<script setup>
import { MotifReviews } from '@thisislefa/motif/vue';
import '@thisislefa/motif/dist/motif.css';

const title = 'Client Reviews';
const ctaText = 'Get Template';
const ctaUrl = '/templates';
const reviews = [
    {
        id: 1,
        company: {
            name: 'Designnest',
            icon: 'fa-border-all'
        },
        rating: 5,
        author: {
            name: 'Emily Davis',
            role: 'Founder, Designnest',
            avatar: 'https://example.com/avatar.jpg'
        },
        content: 'The designs were nothing short of spectacular...'
    }
];

const handleReviewClick = (review) => {
    console.log('Review clicked:', review);
    analytics.track('review_view', { reviewId: review.id });
};
</script>
```

### Angular Component
```typescript
import { Component } from '@angular/core';
import { MotifModule } from '@thisislefa/motif/angular';

@Component({
    selector: 'app-reviews-section',
    standalone: true,
    imports: [MotifModule],
    template: `
        <motif-reviews
            [title]="title"
            [ctaText]="ctaText"
            [ctaUrl]="ctaUrl"
            [reviews]="reviews"
            (reviewClick)="onReviewClick($event)"
        ></motif-reviews>
    `
})
export class ReviewsSectionComponent {
    title = 'Client Reviews';
    ctaText = 'Get Template';
    ctaUrl = '/templates';
    reviews = [
        {
            id: 1,
            company: {
                name: 'Designnest',
                icon: 'fa-border-all'
            },
            rating: 5,
            author: {
                name: 'Emily Davis',
                role: 'Founder, Designnest',
                avatar: 'https://example.com/avatar.jpg'
            },
            content: 'The designs were nothing short of spectacular...'
        }
    ];

    onReviewClick(review: any) {
        console.log('Review clicked:', review);
        this.router.navigate(['/reviews', review.id]);
    }
}
```

## Configuration Options

### Component Properties
```javascript
const config = {
    // Required
    reviews: [
        {
            id: 'unique-id',
            company: {
                name: 'Company Name',
                icon: 'fa-icon-class', // FontAwesome icon class
                logo: 'https://example.com/logo.png', // Optional: image logo
                color: '#4F46E5' // Optional: brand color
            },
            rating: 4.5, // 0-5 scale, supports decimals
            author: {
                name: 'Author Name',
                role: 'Author Role',
                avatar: 'https://example.com/avatar.jpg',
                url: '/author-profile' // Optional: link to author
            },
            content: 'Review text content...',
            
            // Optional metadata
            date: '2024-03-15',
            verified: true,
            featured: false,
            tags: ['design', 'ux', 'web'],
            stats: {
                helpful: 42,
                comments: 5
            }
        }
    ],

    // Optional
    title: 'Client Reviews',
    titleTag: 'h1', // Semantic heading tag (h1-h6)
    ctaText: 'Get Template',
    ctaUrl: '/templates',
    ctaIcon: 'fa-arrow-right',
    maxReviews: 4, // Limit displayed reviews
    showRatings: true,
    showAvatars: true,
    showDates: false,
    sortBy: 'date', // 'date', 'rating', 'helpful'
    order: 'desc', // 'asc' or 'desc'
    
    // Pagination
    pagination: {
        enabled: false,
        pageSize: 4,
        type: 'load-more' // 'load-more' or 'numbered'
    },

    // Events
    onReviewClick: (review) => {},
    onRatingClick: (review, rating) => {},
    onHelpfulClick: (review) => {},

    // Styling
    theme: {
        type: 'light', // 'light', 'dark', or 'custom'
        colors: {
            background: '#ffffff',
            cardBackground: '#F9FAFB',
            textPrimary: '#111827',
            textSecondary: '#6B7280',
            accent: '#000000',
            starFilled: '#000000',
            starEmpty: '#D1D5DB'
        },
        borderRadius: '12px',
        fontFamily: 'Inter, sans-serif'
    }
};
```

### HTML Attributes API
```html
<motif-reviews
    title="Client Reviews"
    cta-text="Get Template"
    cta-url="/templates"
    max-reviews="4"
    show-ratings="true"
    show-avatars="true"
    theme="light"
    data-source="/api/reviews"
    lazy-load="true"
></motif-reviews>
```

## Advanced Features

### Dynamic Data Loading
```javascript
// Load reviews from API
async function loadReviews() {
    const response = await fetch('/api/reviews');
    const data = await response.json();
    
    const component = document.querySelector('motif-reviews');
    component.reviews = data.reviews;
    
    // Or using data attributes for automatic loading
    component.dataset.source = '/api/reviews';
    component.load();
}

// Event listeners for interactivity
document.querySelector('motif-reviews').addEventListener('reviewClick', (event) => {
    const { review, element } = event.detail;
    console.log('Review clicked:', review);
    
    // Track analytics
    analytics.track('review_click', { 
        reviewId: review.id,
        company: review.company.name 
    });
    
    // Open modal or navigate
    if (review.url) {
        window.open(review.url, '_blank');
    }
});

// Rating interaction
document.querySelector('motif-reviews').addEventListener('ratingClick', (event) => {
    const { review, rating } = event.detail;
    
    // Submit rating to API
    fetch(`/api/reviews/${review.id}/rate`, {
        method: 'POST',
        body: JSON.stringify({ rating })
    });
});
```

### Image Optimization
```html
<!-- Lazy loading with modern attributes -->
<div class="cr-profile-wrapper">
    <img 
        src="avatar-placeholder.jpg" 
        data-src="real-avatar.jpg" 
        alt="Emily Davis" 
        class="cr-avatar-img"
        loading="lazy"
        decoding="async"
        width="48"
        height="48"
        sizes="48px"
        srcset="
            avatar-96.jpg 96w,
            avatar-144.jpg 144w
        "
    >
    <!-- Fallback for loading error -->
    <div class="avatar-fallback" aria-hidden="true">
        ED
    </div>
</div>
```

### Accessibility Implementation
```html
<article class="cr-card" 
         role="article"
         aria-labelledby="review-title-1"
         aria-describedby="review-content-1">
    
    <div class="cr-card-header">
        <div class="cr-company-brand" role="group" aria-label="Company information">
            <i class="fa-solid fa-border-all" aria-hidden="true"></i>
            <span id="review-title-1">Designnest</span>
        </div>
        
        <div class="cr-rating-stars" 
             role="img" 
             aria-label="5 out of 5 stars"
             title="5-star rating">
            <!-- Star icons with semantic meaning -->
            <span class="sr-only">Rating: 5 out of 5 stars</span>
            <i class="fa-solid fa-star" aria-hidden="true"></i>
            <i class="fa-solid fa-star" aria-hidden="true"></i>
            <i class="fa-solid fa-star" aria-hidden="true"></i>
            <i class="fa-solid fa-star" aria-hidden="true"></i>
            <i class="fa-solid fa-star" aria-hidden="true"></i>
        </div>
    </div>
    
    <div class="cr-card-body">
        <div class="cr-profile-wrapper" role="group" aria-label="Author information">
            <img src="avatar.jpg" 
                 alt="Headshot of Emily Davis" 
                 class="cr-avatar-img"
                 aria-describedby="author-name-1">
            
            <div class="cr-author-meta">
                <span id="author-name-1" class="cr-author-name">Emily Davis</span>
                <span class="cr-author-role">Founder, Designnest</span>
            </div>
        </div>
        
        <blockquote class="cr-review-content" id="review-content-1">
            "The designs were nothing short of spectacular..."
            <footer class="sr-only">— Emily Davis, Founder at Designnest</footer>
        </blockquote>
    </div>
</article>
```

## Performance Optimization

### Critical CSS Strategy
```html
<style>
/* Inline critical styles for above-the-fold content */
.motif-container {
    opacity: 0;
    animation: fadeIn 0.3s ease forwards;
}

@keyframes fadeIn {
    to { opacity: 1; }
}

/* Load remaining styles asynchronously */
</style>
<link rel="preload" href="motif.css" as="style" onload="this.rel='stylesheet'">
<noscript><link rel="stylesheet" href="motif.css"></noscript>
```

### Lazy Loading Implementation
```javascript
// Intersection Observer for lazy loading
const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            const component = entry.target;
            
            // Load data if using data-source attribute
            if (component.dataset.source && !component.dataset.loaded) {
                component.loadData();
                component.dataset.loaded = 'true';
            }
            
            // Load images
            component.querySelectorAll('img[data-src]').forEach(img => {
                img.src = img.dataset.src;
                img.removeAttribute('data-src');
            });
            
            observer.unobserve(component);
        }
    });
}, { threshold: 0.1 });

// Observe motif components
document.querySelectorAll('motif-reviews[lazy-load]').forEach(component => {
    observer.observe(component);
});
```

## Integration Examples

### CMS Integration (WordPress)
```php
// WordPress shortcode implementation
add_shortcode('motif_reviews', function($atts) {
    $atts = shortcode_atts([
        'title' => 'Client Reviews',
        'max_reviews' => 4,
        'category' => ''
    ], $atts);
    
    // Query reviews from custom post type
    $args = [
        'post_type' => 'review',
        'posts_per_page' => $atts['max_reviews'],
        'meta_key' => 'rating',
        'orderby' => 'meta_value_num',
        'order' => 'DESC'
    ];
    
    if (!empty($atts['category'])) {
        $args['tax_query'] = [
            [
                'taxonomy' => 'review_category',
                'field' => 'slug',
                'terms' => $atts['category']
            ]
        ];
    }
    
    $reviews_query = new WP_Query($args);
    
    ob_start();
    ?>
    <motif-reviews 
        title="<?php echo esc_attr($atts['title']); ?>"
        data-source="<?php echo admin_url('admin-ajax.php?action=get_reviews'); ?>"
    ></motif-reviews>
    <?php
    return ob_get_clean();
});

// AJAX endpoint for dynamic loading
add_action('wp_ajax_get_reviews', 'get_reviews');
add_action('wp_ajax_nopriv_get_reviews', 'get_reviews');

function get_reviews() {
    // Query and return JSON data
    wp_send_json_success($reviews_data);
}
```

### E-commerce Integration (Shopify)
```liquid
{% comment %} Shopify section schema {% endcomment %}
{
  "name": "Motif Reviews",
  "class": "motif-reviews-section",
  "settings": [
    {
      "type": "text",
      "id": "title",
      "label": "Title",
      "default": "Customer Reviews"
    },
    {
      "type": "url",
      "id": "cta_url",
      "label": "CTA Link"
    }
  ],
  "blocks": [
    {
      "type": "review",
      "name": "Review",
      "settings": [
        {
          "type": "text",
          "id": "company",
          "label": "Company Name"
        },
        {
          "type": "range",
          "id": "rating",
          "label": "Rating",
          "min": 1,
          "max": 5,
          "step": 0.5,
          "default": 5
        }
      ]
    }
  ],
  "presets": [
    {
      "name": "Motif Reviews",
      "category": "Content"
    }
  ]
}
```

## Customization & Theming

### CSS Custom Properties
```css
.motif-reviews {
    /* Layout */
    --motif-grid-gap: 24px;
    --motif-card-padding: 32px;
    --motif-internal-gap: 20px;
    
    /* Colors */
    --motif-bg: #ffffff;
    --motif-card-bg: #F9FAFB;
    --motif-text-primary: #111827;
    --motif-text-secondary: #6B7280;
    --motif-text-tertiary: #4B5563;
    --motif-border: #E5E7EB;
    --motif-accent: #000000;
    --motif-star-filled: #000000;
    --motif-star-empty: #D1D5DB;
    --motif-cta-bg: #ffffff;
    --motif-cta-border: #e5e7eb;
    
    /* Typography */
    --motif-font-family: 'Inter', sans-serif;
    --motif-title-size: 48px;
    --motif-review-size: 18px;
    --motif-meta-size: 15px;
    --motif-label-size: 13px;
    
    /* Borders */
    --motif-border-radius: 12px;
    --motif-card-radius: 12px;
    
    /* Animation */
    --motif-transition: 0.2s ease;
    --motif-hover-lift: -2px;
    --motif-hover-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.05);
}

/* Dark theme */
.motif-reviews[theme="dark"] {
    --motif-bg: #111827;
    --motif-card-bg: #1F2937;
    --motif-text-primary: #F9FAFB;
    --motif-text-secondary: #D1D5DB;
    --motif-text-tertiary: #9CA3AF;
    --motif-border: #374151;
    --motif-accent: #FFFFFF;
    --motif-star-filled: #FFFFFF;
    --motif-star-empty: #4B5563;
    --motif-cta-bg: #374151;
    --motif-cta-border: #4B5563;
}

/* Custom theme example */
.motif-reviews.brand-theme {
    --motif-accent: #4F46E5;
    --motif-star-filled: #F59E0B;
    --motif-card-bg: #FEF3C7;
    --motif-border-radius: 16px;
    --motif-title-size: 56px;
}
```

### Component Parts Styling
```css
/* Style internal parts with CSS Shadow Parts */
motif-reviews::part(container) {
    max-width: 1400px;
    margin: 0 auto;
}

motif-reviews::part(header) {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 40px;
}

motif-reviews::part(title) {
    font-size: var(--motif-title-size);
    font-weight: 600;
    letter-spacing: -0.02em;
    color: var(--motif-text-primary);
}

motif-reviews::part(card) {
    background: var(--motif-card-bg);
    border-radius: var(--motif-card-radius);
    padding: var(--motif-card-padding);
    transition: all var(--motif-transition);
}

motif-reviews::part(card-hover) {
    transform: translateY(var(--motif-hover-lift));
    box-shadow: var(--motif-hover-shadow);
}

motif-reviews::part(avatar) {
    width: 48px;
    height: 48px;
    border-radius: 50%;
    object-fit: cover;
}

motif-reviews::part(rating) {
    color: var(--motif-star-filled);
    font-size: 14px;
    letter-spacing: 2px;
}

motif-reviews::part(button) {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 12px 20px;
    background: var(--motif-cta-bg);
    border: 1px solid var(--motif-cta-border);
    border-radius: 6px;
    font-size: 15px;
    font-weight: 600;
    color: var(--motif-text-primary);
    text-decoration: none;
    transition: all var(--motif-transition);
}
```

## Development & Contribution

### Development Setup
```bash
# Clone repository
git clone https://github.com/thisislefa/motif.git
cd motif

# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Run tests
npm test

# Preview production build
npm run preview
```

### Project Structure
```
motif/
├── src/
│   ├── components/          # Web Component source
│   ├── styles/             # CSS and design tokens
│   ├── utils/              # Helper functions
│   ├── index.js            # Main entry point
│   └── motif.js            # Web Component definition
├── dist/                   # Built assets
│   ├── motif.js            # Production JS
│   ├── motif.css           # Production CSS
│   ├── motif.min.js        # Minified version
│   └── motif.min.css       # Minified CSS
├── examples/               # Usage examples
├── tests/                  # Test suites
├── docs/                   # Documentation
├── package.json
└── README.md
```

### Testing Suite
```bash
# Run all tests
npm test

# Run specific test types
npm run test:unit          # Unit tests
npm run test:integration   # Integration tests
npm run test:e2e           # End-to-end tests
npm run test:accessibility # Accessibility tests
npm run test:performance   # Performance tests

# Watch mode for development
npm run test:watch

# Generate coverage report
npm run test:coverage

# Run linting
npm run lint
npm run lint:css
npm run lint:js
```

## Contributing Guide

We welcome contributions from the community! Here's how you can help:

### Ways to Contribute
1. **Report Issues**: Found a bug? Create a detailed issue with reproduction steps
2. **Request Features**: Suggest new features with clear use cases
3. **Improve Documentation**: Help make our docs better for everyone
4. **Submit Code**: Fix bugs or add features via pull requests
5. **Share Examples**: Create implementation examples for different frameworks

### Development Workflow
1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Make your changes following existing patterns
4. Run tests: `npm test`
5. Ensure linting passes: `npm run lint`
6. Commit with descriptive messages: `git commit -m 'Add feature: description'`
7. Push to your fork: `git push origin feature/your-feature`
8. Open a Pull Request with detailed description

### Code Standards
- Follow existing code style and patterns
- Write meaningful commit messages
- Include tests for new features
- Update documentation as needed
- Ensure accessibility compliance (WCAG 2.1 AA)
- Optimize for performance (bundle size, loading speed)
- Maintain browser compatibility (Chrome, Firefox, Safari, Edge)

### Review Process
1. PRs will be reviewed by maintainers
2. Automated checks (tests, linting) must pass
3. Manual review for code quality and standards
4. May request changes or improvements
5. Once approved, will be merged to main branch
6. Included in next release with proper credit

## Support & Community

### Get Help
- **GitHub Issues**: For bug reports and feature requests
- **Discussions**: For questions and community support
- **Documentation**: Complete API reference and guides
- **Examples**: Ready-to-use implementation examples

### Stay Updated
- **GitHub Releases**: Follow releases for updates and changelog
- **Twitter**: Follow [@thisislefa](https://twitter.com/thisislefa) for announcements
- **Newsletter**: Subscribe for major updates and tips

## License
Motif is released under the MIT License. You are free to use, modify, and distribute this component in personal and commercial projects. Attribution is appreciated but not required.

## Acknowledgments
- Built by [Lefa](https://github.com/thisislefa)
- Inspired by modern testimonial design patterns
- Thanks to all contributors and the open source community
- FontAwesome for icons, Inter for typography

