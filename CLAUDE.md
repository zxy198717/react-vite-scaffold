# CLAUDE.md

This file provides guidance to Claude Code when working with this React scaffold.

## Project Overview

A minimal React + TypeScript + Vite starter template. This is a **seed project** - developers will build their own applications on top of this foundation.

## Tech Stack

- **React 19** - UI library
- **TypeScript 5.8** - Type safety
- **Vite 6** - Build tool (fast HMR)
- **Tailwind CSS** - Utility-first CSS (CDN)

## Project Structure

```
src/
├── main.tsx       # React entry point
└── App.tsx        # Root component (Hello World)
```

Simple by design. Developers will add their own components, types, and logic.

## Development Commands

```bash
npm install        # Install dependencies
npm run dev        # Start dev server (http://localhost:3000)
npm run build      # Build for production
npm run preview    # Preview production build
```

## Coding Guidelines

### When Adding Features

1. **Keep It Simple**
   - Start with single-file components
   - Only create folders when you have 3+ related files
   - Avoid premature abstractions

2. **File Organization**
   - Components go in `src/components/`
   - Types go in `src/types/`
   - Utilities go in `src/utils/`
   - Create these folders only when needed

3. **Styling**
   - Use Tailwind utility classes
   - CDN is configured in `index.html`
   - Add custom colors in `tailwind.config` if needed

4. **TypeScript**
   - Always type props and state
   - Use interfaces for props: `interface MyProps {}`
   - Avoid `any` - use `unknown` if necessary

### Component Patterns

**Simple Function Component:**
```typescript
interface MyComponentProps {
  title: string;
  onClick?: () => void;
}

function MyComponent({ title, onClick }: MyComponentProps) {
  return (
    <div className="p-4">
      <h1>{title}</h1>
    </div>
  );
}

export default MyComponent;
```

**With State:**
```typescript
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

### State Management

- Start with `useState` in components
- Lift state to parent when sharing between siblings
- Only add Redux/Zustand when you have complex global state

### Styling Guidelines

**Good:**
```typescript
<div className="flex items-center gap-4 p-6 bg-white rounded-lg shadow">
```

**Avoid:**
```typescript
<div style={{ display: 'flex', padding: '24px' }}> {/* Use Tailwind instead */}
```

### API Integration

When adding API calls:

1. Create `src/services/api.ts`
2. Use environment variables for URLs:
```typescript
const API_URL = import.meta.env.VITE_API_URL || 'http://localhost:4000';
```

3. Add to `.env.local`:
```bash
VITE_API_URL=https://api.example.com
```

### Adding Dependencies

**Think twice before adding:**
- State management libraries (start with useState)
- UI component libraries (Tailwind is enough for most cases)
- Utility libraries (implement simple utils yourself)

**Common useful additions:**
```bash
npm install axios                    # API calls
npm install react-router-dom         # Routing
npm install @tanstack/react-query    # Data fetching
npm install zustand                  # Global state (when needed)
```

## Common Tasks

### Add a New Page

1. Create `src/components/MyPage.tsx`
2. Import and use in `App.tsx`
3. Add routing if needed (install react-router-dom)

### Add Global State

1. Keep it in `App.tsx` until complex
2. Pass down via props
3. Consider Context API before adding Zustand

### Add Styling

- Use Tailwind classes
- Custom colors: edit `tailwind.config` in `index.html`
- Global styles: add to `index.html` `<style>` tag

### Deploy

```bash
npm run build
```

Upload `dist/` folder to:
- Vercel
- Netlify
- GitHub Pages
- Any static host

## What NOT to Do

❌ Don't add unnecessary abstractions
❌ Don't create folders until you have 3+ files
❌ Don't install libraries for simple tasks
❌ Don't use inline styles (use Tailwind)
❌ Don't commit `node_modules` or `dist`
❌ Don't skip TypeScript types

## Architecture Decisions

### Why Vite?
- Fastest dev server
- Best DX for React
- Simple configuration

### Why Tailwind CDN?
- Zero configuration
- Works immediately
- Good for prototypes
- Migrate to PostCSS later if needed

### Why No Router?
- Keep it minimal
- Add react-router-dom when you need multiple pages

### Why No State Library?
- useState is enough to start
- Add Zustand/Redux when complexity requires it

## Performance

### Current Bundle Size
- ~195 KB (61 KB gzipped)
- React 19 + ReactDOM

### Optimization Later
- Code splitting with React.lazy()
- Migrate Tailwind to PostCSS (tree-shaking)
- Add React.memo() for expensive components

## Getting Help

- Vite docs: https://vitejs.dev
- React docs: https://react.dev
- Tailwind docs: https://tailwindcss.com
- TypeScript: https://typescriptlang.org

## Remember

This is a **starting point**, not a framework. Build what you need, when you need it. Keep it simple.
