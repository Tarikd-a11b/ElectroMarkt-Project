# ElectroMart - Web Programming Final Project Report

**Project Name:** ElectroMart - E-Commerce Website for Electrical Supplies  
**Date:** December 2024  
**Course:** Web Programming

---

## Table of Contents
1. [Introduction](#1-introduction)
2. [Design Process](#2-design-process)
3. [Technologies Used](#3-technologies-used)
4. [Functionality](#4-functionality)
5. [Challenges & Solutions](#5-challenges--solutions)
6. [Conclusion](#6-conclusion)

---

## 1. Introduction

### 1.1 Project Overview
ElectroMart is a modern, fully-responsive e-commerce website designed for selling electrical supplies and equipment. The website provides a premium shopping experience with features like product browsing, filtering, cart management, user authentication, and secure checkout.

### 1.2 Objectives
The main objectives of this project are:

- **Create a responsive e-commerce website** - Build a fully functional online store that works seamlessly across desktop, tablet, and mobile devices
- **Implement user authentication** - Provide secure login/registration with both email/password and Google Sign-In options using Firebase Authentication
- **Integrate external APIs** - Utilize real-time currency exchange rates to display prices in multiple currencies
- **Develop a complete shopping experience** - From product browsing to cart management to checkout
- **Apply modern web design principles** - Create a visually appealing dark-themed UI with smooth animations and glassmorphism effects
- **Use localStorage for data persistence** - Store cart items and user preferences locally in the browser

### 1.3 Purpose
The purpose of ElectroMart is to serve as an online platform for purchasing electrical supplies including:
- Cables (HES and ÖZNUR brands)
- Circuit Breakers and RCDs
- Outlets and Switches
- LED Lighting Products
- Electrical Tools and Accessories

---

## 2. Design Process

### 2.1 Wireframes & Structure

The website consists of **8 main pages**:

| Page | File | Purpose |
|------|------|---------|
| Home | `index.html` | Landing page with hero section, featured products, and brand highlights |
| Shop | `shop.html` | Product catalog with filters and sorting |
| Product Detail | `product.html` | Detailed product information page |
| Cart | `cart.html` | Shopping cart with item management |
| Checkout | `checkout.html` | Payment form with credit card preview |
| Login | `login.html` | User authentication (login/register) |
| About | `about.html` | Company information and contact form |
| Product Detail | `product-detail.html` | Individual product display |

### 2.2 Design System

The project implements a comprehensive CSS design system with:

**Color Palette:**
- Primary: `#0066cc` (Blue)
- Secondary: `#ff9500` (Orange)
- Accent: `#00d4aa` (Teal)
- Dark theme with grays: `#1a1a2e` to `#f0f0f8`

**Typography:**
- Primary font: 'Inter' (body text)
- Heading font: 'Outfit' (titles)
- Custom font sizes from `0.75rem` to `3rem`

**Components:**
- Custom buttons with hover effects and gradients
- Product cards with badges and ratings
- Form inputs with focus states
- Modal dialogs for currency selection
- Toast notifications for user feedback

### 2.3 UI/UX Features
- **Dark/Light Theme Toggle** - Users can switch between dark and light modes
- **Responsive Navigation** - Mobile hamburger menu with smooth animations
- **Hero Section** - Gradient background with statistics and call-to-action buttons
- **Product Cards** - Interactive hover effects, badges (New, Popular, Sale)
- **Cart Preview** - Real-time cart count in navigation
- **Credit Card Preview** - Live preview of card details during checkout

---

## 3. Technologies Used

### 3.1 Frontend Technologies

| Technology | Purpose |
|------------|---------|
| **HTML5** | Semantic markup structure |
| **CSS3** | Styling with custom properties, flexbox, and grid |
| **JavaScript (ES6+)** | Client-side interactivity and logic |
| **Google Fonts** | Inter and Outfit typography |

### 3.2 Firebase Integration

```javascript
// Firebase Configuration
const firebaseConfig = {
    apiKey: "AIzaSyC2wkEdH-THvTvvC3FgHt69HPh0kBa5Ugg",
    authDomain: "electromart-34e1c.firebaseapp.com",
    projectId: "electromart-34e1c",
    storageBucket: "electromart-34e1c.firebasestorage.app",
    messagingSenderId: "421141013496",
    appId: "1:421141013496:web:afbbd6bd02aa3dc6e92c0d"
};
```

**Firebase Services Used:**
- **Firebase Authentication** - Email/password and Google Sign-In
- **Firebase SDK v9.22.0** - Compatibility mode for easy implementation

### 3.3 External API Integration

**Exchange Rate API:**
- **URL:** `https://api.exchangerate-api.com/v4/latest/USD`
- **Purpose:** Real-time currency conversion
- **Supported Currencies:** USD, EUR, TRY, GBP, JPY, CHF, CAD, AUD
- **Features:**
  - Response caching (10 minutes) in localStorage
  - Automatic rate refresh
  - Currency selector modal

**API Implementation (api.js):**
```javascript
const API = {
    EXCHANGE_API_URL: 'https://api.exchangerate-api.com/v4/latest/USD',
    CACHE_DURATION: 10 * 60 * 1000, // 10 minutes
    
    currencies: {
        USD: { symbol: '$', name: 'US Dollar', flag: '🇺🇸' },
        EUR: { symbol: '€', name: 'Euro', flag: '🇪🇺' },
        TRY: { symbol: '₺', name: 'Turkish Lira', flag: '🇹🇷' },
        // ... more currencies
    }
};
```

### 3.4 File Structure

```
Web Programming Final Project/
├── index.html          # Homepage
├── shop.html           # Product catalog
├── product.html        # Product detail
├── product-detail.html # Product detail (alternate)
├── cart.html           # Shopping cart
├── checkout.html       # Checkout page
├── login.html          # Authentication
├── about.html          # About us & Contact
├── css/
│   ├── style.css       # Core styles & design tokens
│   ├── components.css  # Reusable component styles
│   ├── layout.css      # Header, footer, navigation
│   ├── pages.css       # Page-specific styles
│   └── forms.css       # Form element styles
├── js/
│   ├── products.js     # Product data (38 products)
│   ├── cart.js         # Cart management
│   ├── auth.js         # Authentication logic
│   ├── api.js          # Currency API integration
│   ├── shop.js         # Shop page filtering/sorting
│   ├── app.js          # Main application logic
│   └── main.js         # Common functionality
└── images/             # Product images (38 files)
```

---

## 4. Functionality

### 4.1 Product Catalog

**38 Products across 8 Categories:**

| Category | Products | Description |
|----------|----------|-------------|
| Cables | 21 | HES and ÖZNUR brand cables (1.5mm² and 2.5mm²) |
| Circuit Breakers | 4 | MCBs and RCDs (16A, 20A, 32A, 30mA) |
| Outlets | 1 | Double socket outlets |
| Switches | 3 | Light switches and dimmers |
| Lighting | 3 | LED bulbs and panels |
| Accessories | 3 | Electrical tape, connectors, junction boxes |
| Tools | 3 | Multimeter, cable stripper, screwdriver set |

**Product Data Structure (products.js):**
```javascript
const products = [
    { 
        id: 1, 
        name: "HES Cable 1.5mm² Brown", 
        brand: "HES", 
        category: "cables",
        thickness: "1.5mm²",
        color: "Brown",
        price: 45.00,
        image: "images/hes 1.5 kahverengi.jpg",
        description: "High-quality HES brand electrical cable...",
        stock: 50,
        unit: "roll",
        badge: null,
        rating: 4.8
    },
    // ... 37 more products
];
```

### 4.2 Shopping Cart Features

**Cart Functionality (cart.js):**
- Add/Remove items from cart
- Update item quantities
- Calculate subtotal, tax (18% VAT), and total
- Persistent storage using localStorage
- Real-time cart count in navigation
- Toast notifications for cart actions

```javascript
const Cart = {
    STORAGE_KEY: 'electromart_cart',
    
    addItem(productId, quantity = 1) { ... },
    removeItem(productId) { ... },
    updateQuantity(productId, quantity) { ... },
    getSubtotal() { ... },
    getTax() { return this.getSubtotal() * 0.18; },
    getTotal() { return this.getSubtotal() + this.getTax(); }
};
```

### 4.3 User Authentication

**Authentication Methods:**
1. **Email/Password Registration** - Create account with Firebase Auth
2. **Email/Password Login** - Sign in with existing credentials
3. **Google Sign-In** - OAuth authentication via Google popup

**User Session Management:**
- User data stored in localStorage
- Profile display in navigation header
- Session persistence across page reloads
- Sign-out functionality

### 4.4 Product Filtering & Search

**Shop Page Features (shop.js):**
- **Search:** Real-time product name search
- **Category Filter:** Filter by cables, breakers, lighting, etc.
- **Brand Filter:** HES, ÖZNUR, or Generic
- **Price Range:** Slider from $0 to $350
- **Sorting Options:** Default, Price (Low/High), Name A-Z, Rating

### 4.5 Checkout Process

**Checkout Features:**
- Order summary with all cart items
- Live credit card preview
- Card number formatting (groups of 4 digits)
- Expiry date formatting (MM/YY)
- CVV validation
- Billing address input
- Order confirmation and cart clearing

### 4.6 Currency Conversion

**Multi-Currency Support:**
- 8 currencies supported (USD, EUR, TRY, GBP, JPY, CHF, CAD, AUD)
- Real-time exchange rates from ExchangeRate-API
- Currency selector modal in header
- Automatic price updates across all pages
- Currency preference saved in localStorage

---

## 5. Challenges & Solutions

### Challenge 1: Real-Time Currency Conversion
**Problem:** Updating all product prices site-wide when the user changes currency without reloading the page.

**Solution:** Implemented a `updateAllPrices()` function that traverses all price elements on the page and converts them based on the selected currency. Original USD prices are stored in `data-usdPrice` attributes for accurate conversions.

### Challenge 2: Cart Persistence
**Problem:** Maintaining cart data across page navigations and browser sessions.

**Solution:** Used `localStorage` to store cart items as a JSON array. The cart is loaded and validated on each page load, with automatic cleanup of invalid items.

### Challenge 3: Firebase Authentication Integration
**Problem:** Integrating multiple authentication methods (email/password and Google) while maintaining a consistent user experience.

**Solution:** Created a unified user data structure stored in localStorage, populated by either authentication method. The UI updates automatically based on authentication state.

### Challenge 4: Responsive Design
**Problem:** Ensuring the website looks and functions well on all device sizes.

**Solution:** Implemented CSS Grid and Flexbox layouts with media queries. The navigation collapses to a hamburger menu on mobile, and the shop layout adjusts from sidebar to stacked layout.

### Challenge 5: Light/Dark Theme Support
**Problem:** Maintaining readability in both themes, especially for elements like the header and footer.

**Solution:** Created CSS custom properties that invert in light mode. The header and footer maintain dark styling in both modes for consistent branding.

### Challenge 6: API Rate Limiting
**Problem:** ExchangeRate-API has rate limits on free tier, causing potential failures on frequent requests.

**Solution:** Implemented a 10-minute cache using localStorage. Cached responses are reused until expired, minimizing API calls.

---

## 6. Conclusion

### 6.1 Project Summary
ElectroMart successfully demonstrates a modern, full-featured e-commerce website built with core web technologies (HTML, CSS, JavaScript). The project showcases:

- **Modern Design:** Premium dark theme with smooth animations and responsive layouts
- **Full Shopping Experience:** Product browsing, filtering, cart management, and checkout
- **Authentication:** Multiple sign-in options using Firebase
- **API Integration:** Real-time currency conversion with caching
- **Best Practices:** Clean code structure, modular JavaScript, and semantic HTML

### 6.2 Features Implemented
- ✅ Responsive design for all devices
- ✅ Product catalog with 38 items
- ✅ Advanced filtering and sorting
- ✅ Shopping cart with localStorage persistence
- ✅ User authentication (Email & Google)
- ✅ Currency exchange API integration
- ✅ Checkout with credit card preview
- ✅ Dark/Light theme toggle
- ✅ Contact form functionality

### 6.3 Future Improvements
Potential enhancements for future versions:
1. Backend integration for order processing
2. Payment gateway integration (Stripe/PayPal)
3. User order history and tracking
4. Product reviews and ratings system
5. Wishlist functionality
6. Email notifications
7. Admin dashboard for product management

### 6.4 Learning Outcomes
Through this project, the following skills were developed and demonstrated:
- **HTML5:** Semantic markup, accessibility, and SEO best practices
- **CSS3:** Modern layout techniques, animations, and responsive design
- **JavaScript:** DOM manipulation, event handling, async/await, and modular code
- **Firebase:** Authentication services and SDK integration
- **API Integration:** Fetching, caching, and error handling for external APIs
- **UI/UX Design:** Creating an intuitive and visually appealing user interface

---

## Appendix

### A. Product Categories
- Cables (21 products)
- Circuit Breakers (4 products)
- Outlets (1 product)
- Switches (3 products)
- Lighting (3 products)
- Accessories (3 products)
- Tools (3 products)

### B. CSS Files Overview
| File | Lines | Purpose |
|------|-------|---------|
| style.css | 248 | Design system, variables, base styles |
| layout.css | ~400 | Header, footer, navigation, grid |
| components.css | ~200 | Buttons, cards, badges |
| pages.css | ~200 | Page-specific layouts |
| forms.css | ~180 | Form inputs and validation |

### C. JavaScript Files Overview
| File | Lines | Purpose |
|------|-------|---------|
| products.js | 82 | Product data array |
| cart.js | 238 | Cart management |
| auth.js | 253 | Authentication logic |
| api.js | 400 | Currency API integration |
| shop.js | ~220 | Product filtering/sorting |
| main.js | ~280 | Theme toggle, navigation |
| app.js | ~480 | Product rendering, utilities |

---

*Report prepared for Web Programming Final Project - December 2024*
