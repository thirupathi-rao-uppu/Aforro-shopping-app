# Aforro - Premium Indian Grocery App

Aforro is a high-fidelity React Native application designed for the Indian grocery market. This repository contains the complete implementation of a modern shopping experience, including dynamic product variants, smart cart management, location-based serviceability checks, and a seamless UPI payment flow.

## 🚀 Key Features

- **Dynamic Product Variants**: Support for multiple weight/quantity options (e.g., 1kg, 2kg, 5kg) with real-time price updates and persistent images.
- **Advanced Cart System**: A variant-aware cart that handles different sizes of the same product as unique items.
- **Location-Based Serviceability**: Integrated address selection with logic to verify if the business provides service to the selected locality.
- **Smart Checkout Flow**:
  - **Auth Guard**: Forces login only when proceeding to pay, ensuring lower friction during browsing.
  - **UPI Integration**: A premium payment selection modal supporting Google Pay, PhonePe, and Paytm with secure transaction simulations.
- **Coupons & Offers**: A horizontal carousel of high-value coupons with automated eligibility checks based on order subtotal.
- **Premium UI/UX**: Custom-designed headers, light-blue savings banners, and smooth transitions matching modern design standards.

## 🛠 Tech Stack

- **Framework**: React Native (CLI)
- **State Management**: [Zustand](https://github.com/pmndrs/zustand) for lean, high-performance global state (Cart & Auth).
- **Navigation**: React Navigation (Native Stack)
- **Icons**: Lucide React Native
- **Design System**: Custom design tokens for colors, spacing, and typography to ensure consistency.

## 📦 Setup Instructions

### Prerequisites

- Node.js >= 22.11.0
- CocoaPods (for iOS)
- Android Studio / Xcode

### Installation

1. **Clone the repository**:
   ```sh
   git clone <repository-url>
   cd Aforro
   ```

2. **Install dependencies**:
   ```sh
   npm install
   ```

3. **Install iOS Pods**:
   ```sh
   cd ios
   pod install
   cd ..
   ```

### Running the App

- **Run on Android**:
  ```sh
  npx react-native run-android
  ```

- **Run on iOS**:
  ```sh
  npx react-native run-ios
  ```

## 🧠 Implementation Approach

### 1. State Management with Zustand
I chose Zustand over Redux for its simplicity and reduced boilerplate.
- **`useCartStore`**: Manages all cart interactions. I implemented a unique keying system `id_variant` to ensure that different weights of the same product are tracked correctly without logical collisions.
- **`useAuthStore`**: A lightweight store to manage user sessions and persistence, allowing for a "browsing-first" experience where users only login when absolutely necessary.

### 2. Deep Linking for Payments
The payment flow implements a simulation of the UPI Intent system.
- It is architected to use standard `upi://pay` URLs, making it trivial to connect to a real merchant VPA in production.
- I used a two-modal approach: one for selection and a second "Loader" modal to build user trust during the simulated handshake with the payment apps.

### 3. Component Architecture
- **Screens**: Dedicated screens for Home, Product Details, Category exploration, and a feature-rich "Review Cart" screen.
- **Theme Engine**: Centralized in `src/theme/tokens.ts`, allowing for global design changes (like the switch to Blue/Green accents) to propagate instantly through the entire app.

### 4. Business Logic (Serviceability & Coupons)
- **Serviceability**: Implemented at the address selection level. When an address is selected, the app performs a recursive check against supported pincodes, updating the UI state globally if a location is unserviceable.
- **Coupon Validator**: A middleware-like function inside the Cart component that validates order subtotals against the `minOrder` requirement of each specific coupon before allowing the discount.

---
*Created with ❤️ for Advanced Agentic Coding.*
