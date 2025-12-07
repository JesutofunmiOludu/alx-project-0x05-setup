# 📘 HookMastery: Unleashing the Power of Hooks

## 📌 Project Description

HookMastery is a Next.js-based web application that allows users to generate AI-powered images using text prompts.  
The app integrates with the GPT-4 Image Generation API and demonstrates clean React architecture using:

- React Hooks (`useState`, `useEffect`)  
- Custom hooks  
- State management across components  
- API routes in Next.js  
- Tailwind CSS for UI  
- TypeScript for type safety  

The project evolves through multiple versions (0x07 → 0x13), each introducing more complex concepts and features.

## 🎯 Learning Objectives

By completing this project, you will learn how to:

- Use the `useState` hook in React  
- Create and use custom React hooks  
- Manage sensitive API keys using environment variables  
- Build and optimize API routes in Next.js  
- Build reusable and typed React components  
- Track and manage application state across multiple components  
- Design responsive interfaces using Tailwind CSS  
- Handle async operations in React  
- Apply React best practices for file structure and component organization  

## 🛠️ Requirements

- Node.js ≥ 14  
- Next.js ≥ 13  
- React ≥ 18  
- TypeScript  
- Tailwind CSS  
- GPT-4 Image Generation API Key (via RapidAPI)  
- Modern Web Browser  

## 📁 Project Structure

```text
alx-project-0x07/ (and subsequent versions)
├── components/
│   ├── common/
│   │   └── ImageCard.tsx
│   └── layouts/
│       ├── Footer.tsx
│       ├── Header.tsx
│       └── Layout.tsx
├── constants/
│   └── index.ts
├── hooks/
│   └── useFetchData.ts
├── interfaces/
│   └── index.ts
├── pages/
│   ├── api/
│   │   └── generate-image.ts
│   ├── _app.tsx
│   └── index.tsx
├── public/
└── styles/
    └── globals.css
```

## ✅ Best Practices Implemented

### 🔹 Component Organization
- Clear separation of layout components (`Header`, `Footer`, `Layout`)  
- Reusable shared components (`ImageCard`)  
- Proper TypeScript typing for all props  

### 🔹 State Management
- `useState` and `useEffect`  
- Custom hooks (`useFetchData`)  
- Type-safe interfaces for state  

### 🔹 API Handling
- Secure server-side API routes  
- Proper error handling & loading states  
- Clean request/response structure  

### 🔹 Security
- API keys stored in `.env.local`  
- Server-side API protects keys  
- Sanitized and typed inputs  

### 🔹 UI/UX
- Fully responsive with Tailwind  
- Clear button states & loading indicators  
- Image gallery with previews  

### 🔹 Type Safety
- Interfaces for components, hooks, API, image objects  
- Generics in custom hooks  
- Strongly typed API responses  

## ⭐ Key Features

### 🖼️ Image Generation
- Enter a text prompt  
- Generate AI-powered images via GPT-4 API  
- Loading feedback while image is generating  

### 🗂️ Image History
- Stores list of all previously generated images  
- Click image to preview full size  

### 🎨 Responsive UI
- Mobile-first layout  
- Clean and intuitive interface  

### 🧩 Custom Hooks
- Shared logic for reusability  
- Built using TypeScript generics  

## 🧬 Development Notes

The app evolves through multiple versions:

- **0x07 – Base Layout**: Next.js project setup, Header, Footer, Layout  
- **0x08 – State Management**: Prompt state, Image tracking, Loading states, ImageCard component  
- **0x09 – Environment Setup**: `.env.local` created, API key securely stored  
- **0x10 – API Integration**: Built `/api/generate-image`, Connected frontend → backend → GPT-4 API  
- **0x11 – Image Tracking**: Store every generated image, Display history list  
- **0x12 – Custom Hooks**: Extracted reusable data-fetching logic  
- **0x13 – Final Polish**: Optimization, Cleaning up structure, Advanced React patterns  

## 🚀 Future Improvements (Optional)

- 🔐 User authentication  
- 💾 Cloud storage for generated images  
- ⚠️ Improved error handling  
- ✂️ Image editing tools  
- 🔗 Social media sharing  
- 🌓 Dark mode  

## 📝 Project Assessment

### ✔️ Manual QA Review (Primary)
Before requesting review:

- Ensure all files are complete  
- Ensure all instructions are followed  
- Generate your review link  
- Submit before the deadline  

### ✔️ Automatic Checks
Will verify:

- Required files exist  
- Environment files ignored  
- Directory structure is correct  

⚠️ Missing the deadline means you can’t generate a review link.

## 🧪 Quiz & Tasks

### <details>
<summary>0. Advanced Image Generation App</summary>

Set up Next.js app and base layout using:

- Header, Footer, Layout, Interfaces  
- Basic Home page with prompt input  

**Example Code Snippet:**

```tsx
// pages/index.tsx
import { useState } from 'react';
import Layout from '../components/layouts/Layout';

export default function Home() {
  const [prompt, setPrompt] = useState('');

  return (
    <Layout>
      <input 
        type="text"
        value={prompt}
        onChange={(e) => setPrompt(e.target.value)}
        placeholder="Enter your prompt"
      />
    </Layout>
  );
}
```

</details>

### <details>
<summary>1. Applying State</summary>

Enhance the Home page to include:

- `prompt`, `imageUrl`, `generatedImages`, `isLoading`  

**Example Code Snippet:**

```tsx
const [imageUrl, setImageUrl] = useState('');
const [generatedImages, setGeneratedImages] = useState<string[]>([]);
const [isLoading, setIsLoading] = useState(false);
```

</details>

### <details>
<summary>2. Local Environment Setup</summary>

- Create `.env.local`  
- Add `NEXT_PUBLIC_GPT_API_KEY`  
- Test via console log  

**Example:**

```env
NEXT_PUBLIC_GPT_API_KEY=your_api_key_here
```

```ts
console.log(process.env.NEXT_PUBLIC_GPT_API_KEY);
```

</details>

### <details>
<summary>3. Generate Image Using API</summary>

- Add constants  
- Create `/api/generate-image.ts`  
- Integrate with GPT-4 Image API  
- Display generated images  

**Example API Route:**

```ts
// pages/api/generate-image.ts
import type { NextApiRequest, NextApiResponse } from 'next';

export default async function handler(req: NextApiRequest, res: NextApiResponse) {
  const { prompt } = req.body;

  const response = await fetch('https://api.openai.com/v1/images', {
    method: 'POST',
    headers: {
      'Authorization': `Bearer ${process.env.NEXT_PUBLIC_GPT_API_KEY}`,
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({ prompt }),
  });

  const data = await response.json();
  res.status(200).json(data);
}
```

</details>

### <details>
<summary>4. Track Generated Images</summary>

- Push each generated image into `generatedImages[]`  
- Display all image history using `ImageCard`  

**Example Code Snippet:**

```tsx
const handleGenerate = async () => {
  setIsLoading(true);
  const res = await fetch('/api/generate-image', {
    method: 'POST',
    body: JSON.stringify({ prompt }),
    headers: { 'Content-Type': 'application/json' },
  });
  const data = await res.json();
  setImageUrl(data.url);
  setGeneratedImages([data.url, ...generatedImages]);
  setIsLoading(false);
};
```

```tsx
{generatedImages.map((img, idx) => (
  <ImageCard key={idx} imageUrl={img} />
))}
```

</details>

## 📂 Repository Information

**GitHub Repo:** alx-project-0x05-setup  

**Directories:**
- alx-project-0x07 → alx-project-0x13
