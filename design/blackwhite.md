# LLM Instructions - Minimalist Black & White Design System

## Overview
This document provides comprehensive instructions for Large Language Models (LLMs) to effectively use and extend this minimalist design system. The system is built with simplicity, consistency, and maintainability as core principles.

## Core Philosophy
When building with this design system, always prioritize:
1. **Minimalism** - Remove unnecessary elements
2. **Clarity** - Make information hierarchy obvious
3. **Consistency** - Use established patterns
4. **White Space** - Let the design breathe
5. **Functionality** - Every element must serve a purpose

## Design Tokens Usage

### Color Palette
```css
/* Primary Usage */
--color-black       /* Primary text, borders, icons */
--color-white       /* Backgrounds, inverted text */
--color-gray-100    /* Subtle backgrounds */
--color-gray-200    /* Default borders */
--color-gray-400    /* Disabled states */
--color-gray-600    /* Secondary text */
```

**Rules:**
- Use pure black (#000) for primary content
- Use grays sparingly for hierarchy
- Never use colors unless explicitly requested
- Borders should be 1px and gray-200 by default

### Typography Scale
```css
/* Use semantic sizing */
--text-base   /* Body text - 16px */
--text-lg     /* Emphasized body - 20px */
--text-xl     /* Small headings - 25px */
--text-2xl    /* Section headings - 31px */
--text-3xl    /* Page headings - 39px */
--text-4xl    /* Hero headings - 49px */
```

**Rules:**
- Body text: Use `--text-base` with `--leading-relaxed`
- Headings: Use `--font-bold` with `--leading-tight`
- Always include proper heading hierarchy (h1 → h6)
- Limit to 2-3 font sizes per component

### Spacing System
```css
/* 4px base unit */
--space-2   /* 8px - Tight spacing */
--space-4   /* 16px - Default spacing */
--space-6   /* 24px - Comfortable spacing */
--space-8   /* 32px - Section spacing */
--space-12  /* 48px - Large gaps */
```

**Rules:**
- Use consistent spacing within components
- Default padding: `--space-4`
- Section margins: `--space-8` or `--space-12`
- Never use arbitrary spacing values

## Component Patterns

### Button Component
```tsx
/* Primary Button */
className="px-6 py-3 bg-black text-white font-medium 
          hover:bg-gray-800 transition-colors duration-200
          focus:outline focus:outline-2 focus:outline-black"

/* Secondary Button */
className="px-6 py-3 bg-white text-black font-medium 
          border border-black hover:bg-gray-100 
          transition-colors duration-200"

/* Ghost Button */
className="px-6 py-3 text-black font-medium 
          hover:bg-gray-100 transition-colors duration-200"
```

### Card Component
```tsx
className="bg-white border border-gray-200 
          p-6 space-y-4"

/* With hover effect */
className="bg-white border border-gray-200 
          p-6 space-y-4 transition-all duration-200
          hover:border-black hover:shadow-md"
```

### Input Component
```tsx
className="w-full px-4 py-2 border border-gray-200 
          focus:border-black focus:outline-none
          transition-colors duration-200
          placeholder:text-gray-400"
```

### Layout Containers
```tsx
/* Full-width container with padding */
className="w-full max-w-7xl mx-auto px-4 sm:px-6 lg:px-8"

/* Content container */
className="max-w-4xl mx-auto"

/* Narrow container for forms */
className="max-w-md mx-auto"
```

## Common Layouts

### Hero Section
```tsx
<section className="min-h-screen flex items-center justify-center px-4">
  <div className="max-w-4xl mx-auto text-center space-y-8">
    <h1 className="text-4xl md:text-5xl font-bold leading-tight">
      {title}
    </h1>
    <p className="text-lg md:text-xl text-gray-600 max-w-2xl mx-auto">
      {description}
    </p>
    <div className="flex gap-4 justify-center">
      {/* Buttons */}
    </div>
  </div>
</section>
```

### Dashboard Layout
```tsx
<div className="min-h-screen flex">
  {/* Sidebar */}
  <aside className="w-64 border-r border-gray-200 p-6">
    {/* Navigation */}
  </aside>
  
  {/* Main Content */}
  <main className="flex-1 p-8">
    <div className="max-w-6xl mx-auto space-y-8">
      {/* Content */}
    </div>
  </main>
</div>
```

### Grid Layout
```tsx
/* 2 Column */
className="grid grid-cols-1 md:grid-cols-2 gap-6"

/* 3 Column */
className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6"

/* 4 Column */
className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6"
```

## State Patterns

### Hover States
- Buttons: Darken background slightly or add border
- Cards: Add black border or subtle shadow
- Links: Reduce opacity to 0.7
- Always include transition for smooth effect

### Focus States
- Always include visible focus indicators
- Use 2px black outline with 2px offset
- Never remove focus states

### Disabled States
```tsx
className="opacity-50 cursor-not-allowed pointer-events-none"
```

### Loading States
```tsx
/* Spinner */
<div className="animate-spin h-5 w-5 border-2 
              border-gray-300 border-t-black rounded-full" />

/* Skeleton */
<div className="animate-pulse bg-gray-200 h-4 w-full rounded" />
```

## Responsive Design Rules

### Breakpoints
- Mobile First approach always
- sm: 640px
- md: 768px  
- lg: 1024px
- xl: 1280px
- 2xl: 1536px

### Common Responsive Patterns
```tsx
/* Text sizing */
className="text-base md:text-lg lg:text-xl"

/* Padding */
className="p-4 md:p-6 lg:p-8"

/* Grid columns */
className="grid-cols-1 md:grid-cols-2 lg:grid-cols-3"

/* Hide/Show */
className="hidden md:block"  /* Hide on mobile */
className="md:hidden"        /* Show only on mobile */
```

## Animation Guidelines

### Allowed Animations
```css
/* Transitions */
transition-all duration-200
transition-colors duration-150
transition-opacity duration-300

/* Transforms */
hover:scale-105
hover:-translate-y-1

/* Keyframes (use sparingly) */
animate-pulse  /* Loading states */
animate-spin   /* Spinners */
```

**Rules:**
- Keep animations subtle and functional
- Duration: 150-300ms for micro-interactions
- Use ease or ease-in-out timing functions
- Avoid bouncy or playful animations

## Component Composition

### When Building New Components
1. Start with semantic HTML
2. Apply base styles from design tokens
3. Add interactive states (hover, focus, active)
4. Ensure responsive behavior
5. Test accessibility

### Example Component Structure
```tsx
// Component.tsx
import React from 'react';
import styles from './Component.module.css';

interface ComponentProps {
  children: React.ReactNode;
  variant?: 'primary' | 'secondary';
  className?: string;
}

export const Component: React.FC<ComponentProps> = ({ 
  children, 
  variant = 'primary',
  className = '' 
}) => {
  const baseStyles = 'base-styles-here';
  const variantStyles = {
    primary: 'primary-styles',
    secondary: 'secondary-styles'
  };
  
  return (
    <div className={`${baseStyles} ${variantStyles[variant]} ${className}`}>
      {children}
    </div>
  );
};
```

## File Naming Conventions

### Components
- PascalCase: `Button.tsx`, `Card.tsx`
- Index exports: `components/ui/index.ts`

### Styles
- Lowercase: `globals.css`, `typography.css`
- CSS Modules: `Button.module.css`

### Utilities
- camelCase: `formatDate.ts`, `parseData.ts`

### Pages/Examples
- kebab-case: `landing-page.tsx`, `dashboard-view.tsx`

## Common Pitfalls to Avoid

### DON'T:
- Add colors beyond black/white/gray
- Use shadows excessively
- Create overly complex layouts
- Add decorative elements without purpose
- Use inconsistent spacing
- Forget hover/focus states
- Ignore responsive design
- Over-animate interfaces

### DO:
- Maintain visual hierarchy through size and weight
- Use consistent spacing throughout
- Ensure all interactive elements have states
- Test on multiple screen sizes
- Keep components simple and reusable
- Document component usage
- Follow established patterns

## Extending the System

### Adding New Components
1. Check if existing components can be composed
2. Follow the established visual language
3. Use only existing design tokens
4. Document the component purpose and usage
5. Include all necessary states

### Modifying Existing Components
1. Maintain backward compatibility
2. Update documentation
3. Test across all usage instances
4. Preserve accessibility features

## Accessibility Checklist
- [ ] Semantic HTML elements used
- [ ] ARIA labels where needed
- [ ] Keyboard navigation works
- [ ] Focus indicators visible
- [ ] Color contrast meets WCAG AA
- [ ] Interactive elements have hover/focus states
- [ ] Form inputs have labels
- [ ] Error messages are clear

## Quick Reference

### Essential Classes (Tailwind)
```css
/* Layout */
flex items-center justify-center
grid grid-cols-{n} gap-{n}
max-w-{size} mx-auto

/* Spacing */
p-{n} m-{n} space-y-{n} gap-{n}

/* Typography */
text-{size} font-{weight} leading-{height}

/* Borders */
border border-gray-200 rounded-{size}

/* States */
hover: focus: active: disabled:

/* Responsive */
sm: md: lg: xl: 2xl:
```

## Testing Your Implementation

Before considering a component complete:
1. Review against the design principles
2. Check responsive behavior
3. Test all interactive states
4. Verify accessibility
5. Ensure consistent spacing
6. Validate semantic HTML usage

Remember: When in doubt, choose simplicity. The best interface is often the one with the least elements that still accomplishes the user's goal effectively.
