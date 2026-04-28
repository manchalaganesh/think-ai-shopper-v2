
## ThinkBold — Gen-Z Streetwear Store + ThinkAi Chatbot

A bold, trendy clothing e-commerce site (demo catalog) with an AI customer service chatbot called **ThinkAi**, powered by Lovable AI.

### 🎨 Visual Style
- **Vibe:** Gen-Z streetwear — vibrant accent color (electric lime/magenta), bold oversized typography, dark sections mixed with bright pops, playful chunky borders, sticker-style badges ("NEW", "🔥 HOT").
- **Typography:** Display sans (Space Grotesk / Archivo Black) for headers, clean sans for body.
- **Layout:** Asymmetric grids, large product imagery, marquee scrolling text, hover animations.

### 🛍️ Pages & Routes
1. **Home** — Hero with animated tagline, featured drops, marquee, category tiles (Men / Women / Accessories), trending products, brand story strip.
2. **Shop (`/shop`)** — Full catalog with filters (category, size, price) and sort.
3. **Categories** — `/men`, `/women`, `/accessories` with category-specific hero + product grid.
4. **Product Detail (`/product/$id`)** — Image gallery, size selector, price, description, "Add to cart", related products.
5. **Cart (`/cart`)** — Line items, qty controls, subtotal, mock "Checkout" (shows success modal — no real payment).
6. **About (`/about`)** — Brand story, mission, values, team blurb.
7. **Contact (`/contact`)** — Contact form (validated with zod) + social links.
8. **Auth (`/login`, `/signup`)** — Email/password via Lovable Cloud auth. Saves cart + chat history per user.
9. **Account (`/account`)** — Order history (mock), saved chats, profile.

### 🤖 ThinkAi Chatbot (Floating Widget on Every Page)
- **Floating button** bottom-right with bold ThinkAi branding + pulse animation.
- **Chat panel** opens with greeting, suggested prompts ("Recommend an outfit", "What's your return policy?", "Track my order").
- **Capabilities (all powered by Lovable AI Gateway via edge function):**
  - **Product recommendations** — AI receives the catalog as context and suggests items based on user requests (e.g., "I need streetwear for a summer party"). Recommended products render as clickable cards inside the chat.
  - **FAQs** — Pre-loaded knowledge: shipping, returns (30 days), sizing guide, payment, materials.
  - **Order/product lookup** — Tool calling to query mock order DB and product catalog.
  - **General conversation with memory** — Full conversation history sent each turn; persisted per user (or per session for guests) in Lovable Cloud.
- **Tech:** Streaming responses (token-by-token), markdown rendering, tool calling for structured product cards, handles 429/402 errors with friendly toasts.
- **Model:** `google/gemini-3-flash-preview` (fast + free tier friendly).

### 🗄️ Database (Lovable Cloud)
- `profiles` (user info)
- `products` (seeded clothing catalog with images, sizes, category)
- `orders` + `order_items` (mock order history per user)
- `chat_conversations` + `chat_messages` (persisted ThinkAi history)
- `cart_items` (saved cart per logged-in user)
- RLS on all tables — users only see their own data.

### 🔐 Auth
- Email/password signup/login (auto-confirm enabled for demo).
- Guest browsing supported; cart and chat persist after login.
- Profiles auto-created via trigger on signup.

### ✅ Security
- Zod validation on all forms (contact, auth, chat input).
- AI calls only via edge function — `LOVABLE_API_KEY` never exposed.
- RLS policies on every table.
- Rate-limit error surfacing with user-friendly toasts.

### 📦 Deliverables in This Build
- Complete storefront with 8+ pages and ~12 seeded clothing products with real imagery.
- Working cart + mock checkout flow.
- Fully functional ThinkAi chatbot with streaming, product recommendations via tool calling, persistent memory, and FAQ knowledge.
- Auth + per-user data persistence.
- Mobile-responsive (tested on 304px viewport you're previewing).
