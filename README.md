<div align="center">

<img src="public/orange-logo.png" alt="Servd Logo" width="80" />

# 🍽️ Servd — AI-Powered Recipe Platform

**Discover recipes from what's already in your kitchen.**

[![Next.js](https://img.shields.io/badge/Next.js-15-black?style=flat-square&logo=next.js)](https://nextjs.org/)
[![Strapi](https://img.shields.io/badge/Strapi-CMS-4945FF?style=flat-square&logo=strapi)](https://strapi.io/)
[![Clerk](https://img.shields.io/badge/Auth-Clerk-6C47FF?style=flat-square&logo=clerk)](https://clerk.com/)
[![Google Gemini](https://img.shields.io/badge/AI-Gemini-4285F4?style=flat-square&logo=google)](https://ai.google.dev/)
[![Vercel](https://img.shields.io/badge/Deployed-Vercel-000?style=flat-square&logo=vercel)](https://vercel.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg?style=flat-square)](LICENSE)

[🚀 Live Demo](https://servd-ai-recipe-platform-rho.vercel.app/) · [📁 Repository](https://github.com/Saket22-CS/AI_Recipe_Platform.git)

</div>

---

## 📸 Overview

**Servd** is a fullstack, AI-powered recipe platform that transforms your pantry into a personalized meal planner. Upload a photo of your fridge or pantry, and the platform's AI engine identifies your ingredients and generates custom recipes tailored to what you actually have at home - reducing food waste and making cooking effortless.

Beyond pantry scanning, Servd offers a rich browsing experience with thousands of recipes organized by cuisine, category, and mood, an AI chef for on-demand cooking instructions, nutritional breakdowns, smart ingredient substitutions, PDF exports, and personal recipe collections.

---

## ✨ Features

### 🧠 AI-Powered Pantry Scanning
- Upload a photo of your pantry or fridge
- Google Gemini analyzes the image and extracts ingredient names, quantities, and confidence scores
- Generates fully detailed recipes based on detected ingredients
- Manually add, edit, or delete pantry items as well

### 🍲 Recipe Exploration
- Browse a large recipe library via the MealDB API — filtered by category, cuisine, and country
- **Recipe of the Day** — a daily random recipe, cached for 24 hours
- **How to Cook** — ask the AI chef for step-by-step instructions for any dish in the world
- Recipe cards with prep/cook time, servings, ingredients, and images from Unsplash

### 📋 Full Recipe Details
- Complete ingredient lists with quantities
- Numbered step-by-step cooking instructions with pro tips
- Nutritional breakdown *(Pro)*
- Smart ingredient substitutions *(Pro)*
- Export any recipe as a downloadable PDF

### 💾 My Recipes Collection
- Save and unsave recipes to a personal collection
- View your saved recipes anytime from a dedicated page

### 💳 Subscription Plans

| Feature | Free | Pro ($7.99/mo) |
|---|---|---|
| Pantry Scans / Month | 10 | Unlimited |
| AI Meal Recommendations | 5 | Unlimited |
| Recipe Library | ✅ | ✅ |
| Nutritional Info | ❌ | ✅ |
| Ingredient Substitutions | ❌ | ✅ |
| PDF Export | ✅ | ✅ |
| Priority Support | ❌ | ✅ |

### 🔐 Authentication & Billing
- Sign in with Google or email/password via Clerk
- Full user profile management (name, email, security settings)
- In-app billing & subscription management — no external portal needed

### 🛡️ Security & Rate Limiting
- Bot detection and blocking via Arcjet
- Shield protection against SQL injection and XSS attacks
- Tier-based rate limiting — free vs. pro users get separate API quotas
- Analytics and real-time request monitoring

---

## 🗂️ Project Structure

```
frontend/
├── actions/                  # Servdr actions (pantry, recipes, mealdb)
├── app/
│   ├── (auth)/               # Sign-in / Sign-up pages (Clerk)
│   ├── (main)/
│   │   ├── dashboard/        # User dashboard
│   │   ├── pantry/           # Pantry management & AI-generated recipes
│   │   ├── recipe/           # Single recipe detail page
│   │   └── recipes/          # Browse all recipes (category & cuisine filters)
│   ├── globals.css
│   └── layout.js
├── components/
│   ├── ui/                   # shadcn/ui base components (button, card, dialog, tabs…)
│   ├── Header.jsx
│   ├── AddToPantryModal.jsx
│   ├── HowToCookModal.jsx
│   ├── ImageUploader.jsx
│   ├── PricingModal.jsx
│   ├── RecipeCard.jsx
│   ├── RecipeGrid.jsx
│   ├── RecipePDF.jsx
│   └── UserDropdown.jsx
├── hooks/
│   └── use-fetch.js          # Custom hook for data fetching with loading & error state
├── lib/
│   ├── arcjet.js             # Rate limiting & bot protection config
│   ├── checkUser.js          # Clerk user sync to Strapi DB
│   ├── data.js               # Static data helpers
│   └── utils.js              # Utility functions
└── public/                   # Static assets (logos, images)
```

---

## 🛠️ Tech Stack

### Frontend
| Technology | Purpose |
|---|---|
| [Next.js 15](https://nextjs.org/) | React framework with App Router, SSR, and Servdr Actions |
| [Tailwind CSS](https://tailwindcss.com/) | Utility-first CSS framework |
| [shadcn/ui](https://ui.shadcn.com/) | Accessible, reusable UI component library |
| [Lucide React](https://lucide.dev/) | Icon library |
| [react-dropzone](https://react-dropzone.js.org/) | Drag-and-drop image upload |
| [react-pdf/renderer](https://react-pdf.org/) | Client-side PDF generation |

### Backend & Database
| Technology | Purpose |
|---|---|
| [Strapi](https://strapi.io/) | Headless CMS for content management and REST API |
| [Neon](https://neon.tech/) | Servdrless PostgreSQL database |

### AI & External APIs
| Technology | Purpose |
|---|---|
| [Google Gemini](https://ai.google.dev/) | Pantry image recognition & recipe generation |
| [MealDB API](https://www.themealdb.com/api.php) | Recipe browsing — categories and cuisines |
| [Unsplash API](https://unsplash.com/developers) | Dynamic recipe imagery |

### Auth, Billing & Security
| Technology | Purpose |
|---|---|
| [Clerk](https://clerk.com/) | Authentication, user management, and billing |
| [Arcjet](https://arcjet.com/) | Rate limiting, bot protection, and attack shielding |

### Deployment
| Service | Role |
|---|---|
| [Vercel](https://vercel.com/) | Frontend hosting with CI/CD |
| [Strapi Cloud](https://cloud.strapi.io/) | Backend CMS hosting |

---

## 🗄️ Database Schema

```
users
  ├── id
  ├── clerkId       (unique Clerk user identifier)
  ├── email
  ├── firstName / lastName
  ├── imageUrl
  └── subscriptionTier  (free | pro)

pantryItems
  ├── id
  ├── name
  ├── quantity
  ├── imageUrl      (optional)
  └── owner         → users.id

recipes
  ├── id
  ├── author        → users.id
  ├── title / description
  ├── cuisine / category  (enums)
  ├── ingredients   (JSON array)
  ├── instructions  (JSON)
  ├── imageUrl
  ├── prepTime / cookTime / servings
  ├── nutrition     (JSON — pro feature)
  ├── tips          (JSON)
  ├── substitutions (JSON)
  └── isPublic      (boolean)

savedRecipes
  ├── id
  ├── user          → users.id
  ├── recipe        → recipes.id
  └── savedAt       (datetime)
```

---

## 🤖 AI Prompt Design

**Pantry Image Recognition**
- Instructs Gemini to identify all visible food items in the uploaded image
- Returns a JSON array: `[{ name, quantity, confidence }]`
- Ignores non-food items and estimates quantities from visual cues

**Recipe Generation**
- Provides ingredient list from pantry scan as context
- Returns a structured JSON object with `title`, `description`, `category`, `cuisine`, `ingredients`, `instructions`, `nutrition`, `tips`, and `substitutions`
- Enforces realistic outputs with rules to prevent hallucinated ingredients
- Includes few-shot examples for categories and cuisines

---

## 🚀 Getting Started

### Prerequisites
- Node.js 18+
- A Neon PostgreSQL database
- Clerk account (for auth & billing)
- Google Gemini API key
- Arcjet API key
- Unsplash API key

### 1. Clone the Repository

```bash
git clone https://github.com/Saket22-CS/AI_Recipe_Platform.git
cd AI_Recipe_Platform/frontend
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment Variables

Create a `.env.local` file in the `frontend` directory:

```env
# Clerk
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
CLERK_SECRET_KEY=your_clerk_secret_key
NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up

# Strapi Backend
NEXT_PUBLIC_STRAPI_URL=http://localhost:1337
STRAPI_API_TOKEN=your_strapi_api_token

# Google Gemini
GEMINI_API_KEY=your_gemini_api_key

# Unsplash
UNSPLASH_ACCESS_KEY=your_unsplash_access_key

# Arcjet
ARCJET_KEY=your_arcjet_key
```

### 4. Run the Development Servdr

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### 5. Backend Setup (Strapi)

```bash
cd ../backend   # or your Strapi project root
npm install
npm run develop
```

Configure the database connection in Strapi to point to your Neon PostgreSQL instance, then set up the content types and permissions as described in the [Database Schema](#️-database-schema) section above.

---

## 🔒 Security Details

Arcjet is integrated into the Next.js middleware layer and applied to all API routes and server actions:

- **Rate Limiting** — Free users: 10 pantry scans/month, 5 meal recommendations/month. Pro users: up to 1000 requests/day.
- **Bot Protection** — Allows verified crawlers (e.g. Googlebot) while blocking malicious bots.
- **Shield Mode** — Automatically blocks requests matching SQL injection and XSS patterns.
- **Real-time Analytics** — Monitor API usage and threat activity from the Arcjet dashboard.

---

## 📦 Key Scripts

```bash
npm run dev        # Start development server
npm run build      # Build for production
npm run start      # Run production build locally
npm run lint       # Run ESLint
```

---

## 🌐 Deployment

### Frontend (Vercel)
1. Push the repo to GitHub.
2. Import the project into [Vercel](https://vercel.com/).
3. Add all environment variables under **Project Settings → Environment Variables**.
4. Deploy — Vercel automatically handles builds on every push to `main`.

### Backend (Strapi Cloud)
1. Create a project on [Strapi Cloud](https://cloud.strapi.io/).
2. Connect your GitHub repository.
3. Set all environment variables (database URL, API tokens).
4. Deploy — Strapi Cloud provisions the CMS and exposes the REST API.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

## 🙋‍♂️ Author

**Saket** — [@Saket22-CS](https://github.com/Saket22-CS)

If you found this project useful, please consider giving it a ⭐ on [GitHub](https://github.com/Saket22-CS/AI_Recipe_Platform.git)!

---

<div align="center">
  <sub>Built with ❤️ using Next.js, Google Gemini, and Strapi</sub>
</div>