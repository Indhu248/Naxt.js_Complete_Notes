In Next.js, routing and metadata management are handled in a structured way, especially in the **App Router** introduced in Next.js 13+ (`app/` directory structure). Here's a breakdown of both:

---

## 🛣️ **Routing in Next.js (App Router)**

### 1. **Pages and Layouts Structure**
- Files in `app/` become routes automatically.
- Example structure:
  ```
  app/
    page.tsx         --> route: /
    about/
      page.tsx       --> route: /about
    blog/
      [slug]/
        page.tsx     --> dynamic route: /blog/my-article
  ```

### 2. **Dynamic Routing**
- Use square brackets:
  ```bash
  app/blog/[slug]/page.tsx → /blog/hello-world
  ```

### 3. **Catch-all Routes**
- For nested paths:
  ```bash
  app/docs/[...slug]/page.tsx → /docs/a/b/c
  ```

---

## 🧠 **Metadata in Next.js (SEO, Titles, etc.)**

### Option 1: **Static Metadata (Exported Object)**
For simple, static metadata:

```tsx
// app/about/page.tsx
export const metadata = {
  title: "About Us",
  description: "Learn more about our team.",
};
```

### Option 2: **Dynamic Metadata Function**
Useful for dynamic routes:

```tsx
// app/blog/[slug]/page.tsx
import { getPost } from "@/lib/api";

export async function generateMetadata({ params }) {
  const post = await getPost(params.slug);
  return {
    title: post.title,
    description: post.excerpt,
  };
}
```

---

### ✅ Available Metadata Fields:
You can use fields like:
```ts
export const metadata = {
  title: "Page Title",
  description: "Page description",
  keywords: ["keyword1", "keyword2"],
  authors: [{ name: "Indu", url: "https://example.com" }],
  openGraph: {
    title: "OG Title",
    description: "OG Description",
    url: "https://example.com/page",
    siteName: "Site Name",
    images: [
      {
        url: "https://example.com/image.jpg",
        width: 800,
        height: 600,
        alt: "Image description",
      },
    ],
    locale: "en_US",
    type: "website",
  },
};
```

---
