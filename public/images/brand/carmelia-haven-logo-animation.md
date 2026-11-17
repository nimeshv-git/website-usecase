# Carmelia Haven Official Animated Logo Documentation

This document records the official rotating/animated logo extracted directly from the live Carmelia Haven website (`https://www.carmeliahaven.com/index.php`).

> [!NOTE]
> Per project instructions, **none of the existing website components, navbars, headers, footers, or pages have been modified**. All assets have been saved strictly inside `public/images/brand/` for future reference and optional integration.

---

## 1. Asset & Source Overview

| Specification | Value |
| :--- | :--- |
| **Official Website** | `https://www.carmeliahaven.com/index.php` |
| **Original Outer Ring Asset** | `https://www.carmeliahaven.com/images_ch/rorate_logo_01.png` |
| **Original Central Emblem Asset** | `https://www.carmeliahaven.com/images_ch/rorate_logo_02.png` |
| **Official Header Vector Logo** | `https://www.carmeliahaven.com/images_ch/logo_carmeliahaven.svg` |
| **Official Footer Emblem** | `https://www.carmeliahaven.com/images_ch/logo_emblem_carmeliahaven.png` |
| **Original Asset Format** | PNG with RGBA alpha transparency (164 &times; 164 px) |
| **Animation Mechanism** | **CSS Animation** (`@keyframes rotation` / `-webkit-animation`) |
| **Rotation Direction** | **Clockwise** (`0deg` to `359deg` / `360deg`) |
| **Animation Duration** | **8 seconds** (8000ms per full 360&deg; revolution) |
| **Animation Timing Function** | `linear` (smooth constant velocity, no easing jump) |
| **Animation Looping** | `infinite` (seamless continuous loop) |

---

## 2. How the Original Website Implements the Animation

On the official website (in the welcome/story section), the rotating emblem is constructed using **two overlapping layers**:

1. **Central Layer (`rorate_logo_02.png`):** A static tree/plantation emblem pinned in the exact center.
2. **Outer Layer (`rorate_logo_01.png`):** A circular ring featuring the typography, rotating continuously around the central emblem.

### Original HTML Structure:
```html
<div class="position-relative d-md-flex flex-column align-items-center justify-content-center w-165px h-165px border-radius-100">
    <!-- Static center emblem -->
    <img src="images_ch/rorate_logo_02.png" class="position-absolute top-50 translate-middle-y" alt="Carmelia Haven Emblem">
    <!-- Continuously rotating outer typography ring -->
    <img src="images_ch/rorate_logo_01.png" class="animation-rotation" alt="Carmelia Haven Rotating Ring">
</div>
```

### Original CSS Rules (from `css/style.css`):
```css
.animation-rotation {
    -webkit-animation: rotation 8s infinite linear;
    animation: rotation 8s infinite linear;
}

@-webkit-keyframes rotation {
    from {
        -webkit-transform: rotate(0deg);
    }
    to {
        -webkit-transform: rotate(359deg);
    }
}

@keyframes rotation {
    from {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(359deg);
    }
}
```

---

## 3. Local Files Saved in `public/images/brand/`

All original and derived assets have been downloaded and generated locally:

1. **Original Raw Assets:**
   - [rorate_logo_01.png](file:///d:/OneDrive%20-%2010xDS/Desktop/Carmelia%20Haven/public/images/brand/rorate_logo_01.png) & [carmelia-haven-rotating-ring.png](file:///d:/OneDrive%20-%2010xDS/Desktop/Carmelia%20Haven/public/images/brand/carmelia-haven-rotating-ring.png) *(7.4 KB, 164 &times; 164 px)*
   - [rorate_logo_02.png](file:///d:/OneDrive%20-%2010xDS/Desktop/Carmelia%20Haven/public/images/brand/rorate_logo_02.png) & [carmelia-haven-rotating-center.png](file:///d:/OneDrive%20-%2010xDS/Desktop/Carmelia%20Haven/public/images/brand/carmelia-haven-rotating-center.png) *(4.0 KB, 164 &times; 164 px)*
   - [logo_carmeliahaven.svg](file:///d:/OneDrive%20-%2010xDS/Desktop/Carmelia%20Haven/public/images/brand/logo_carmeliahaven.svg) *(46.3 KB)*
   - [logo_emblem_carmeliahaven.png](file:///d:/OneDrive%20-%2010xDS/Desktop/Carmelia%20Haven/public/images/brand/logo_emblem_carmeliahaven.png) *(10.6 KB)*

2. **Standalone Animated Logo Formats (for direct use without multi-layer CSS):**
   - [carmelia-haven-animated-logo.gif](file:///d:/OneDrive%20-%2010xDS/Desktop/Carmelia%20Haven/public/images/brand/carmelia-haven-animated-logo.gif) *(167.8 KB, 40-frame GIF, 8s loop, transparent background)*
   - [carmelia-haven-animated-logo.webp](file:///d:/OneDrive%20-%2010xDS/Desktop/Carmelia%20Haven/public/images/brand/carmelia-haven-animated-logo.webp) *(730.4 KB, 60-frame WebP with 8-bit alpha channel transparency)*
   - [carmelia-haven-animated-logo.svg](file:///d:/OneDrive%20-%2010xDS/Desktop/Carmelia%20Haven/public/images/brand/carmelia-haven-animated-logo.svg) *(15.8 KB, standalone vector SVG with embedded CSS animation)*

3. **Interactive Local Verification Preview:**
   - [carmelia-haven-logo-preview.html](file:///d:/OneDrive%20-%2010xDS/Desktop/Carmelia%20Haven/public/images/brand/carmelia-haven-logo-preview.html) *(Double-click to open in any web browser to view the side-by-side comparison on dark and light surfaces)*

---

## 4. How to Use in Next.js / Tailwind CSS (When Needed in the Future)

### Method A: Standalone SVG (Recommended for best sharpness and zero CPU overhead)
```tsx
import Image from "next/image";

export const BrandRotatingBadge = ({ size = 120 }: { size?: number }) => (
  <Image
    src="/images/brand/carmelia-haven-animated-logo.svg"
    alt="Carmelia Haven"
    width={size}
    height={size}
    priority
  />
);
```

### Method B: Native Tailwind CSS Layered Approach (Exact match to original site)
```tsx
import Image from "next/image";

export const RotatingEmblem = ({ size = 120 }: { size?: number }) => {
  return (
    <div
      className="relative flex items-center justify-center select-none"
      style={{ width: size, height: size }}
    >
      {/* Static Central Emblem */}
      <Image
        src="/images/brand/carmelia-haven-rotating-center.png"
        alt="Carmelia Haven Emblem"
        fill
        className="object-contain p-2"
      />
      {/* Continuously Rotating Outer Typography Ring */}
      <div className="absolute inset-0 animate-[spin_8s_linear_infinite]">
        <Image
          src="/images/brand/carmelia-haven-rotating-ring.png"
          alt="Carmelia Haven"
          fill
          className="object-contain"
        />
      </div>
    </div>
  );
};
```

