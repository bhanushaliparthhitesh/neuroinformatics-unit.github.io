# Sidebar Navigation Component

## Overview
This is a framework-agnostic, standalone left sidebar navigation component inspired by the PyData Sphinx Theme (as seen on the Panel documentation site). It features grouped sections, expandable navigation menus, a bottom project switcher dropdown, and a fully responsive off-canvas mobile layout.

## Features List
- **Grouped Sections**: Uppercase, muted section labels (e.g., "FOR USERS", "FOR DEVELOPERS").
- **Expandable Items**: Accordion-style navigation lists with chevron icons that smoothly rotate on toggle.
- **Active & Hover States**: PyData Sphinx Theme styling (light gray background on hover, blue accent color on active).
- **Project Switcher Dropdown**: A bottom-anchored menu allowing users to switch between related documentation sites or projects.
- **Responsive / Mobile-Ready**: Automatically collapses into a hidden off-canvas menu on smaller screens, toggled by a hamburger button with a darkened overlay.

## File Structure
By default, this component can be embedded into a single `.html` file. However, for a cleaner architecture in larger projects, it is recommended to split it into three standard web files:
- `sidebar.html` (DOM Structure)
- `sidebar.css` (Styling & CSS Variables)
- `sidebar.js` (DOM interactivity, toggle states)

## Full Code Blocks

### HTML (`sidebar.html`)
```html
<!-- Mobile Toggle Button -->
<button class="mobile-toggle" id="mobileToggle" aria-label="Toggle Navigation">
  <i class="fa-solid fa-bars"></i>
</button>

<!-- Mobile Overlay -->
<div class="sidebar-overlay" id="sidebarOverlay"></div>

<!-- The Sidebar -->
<aside class="sidebar" id="sidebar">
  <div class="sidebar-content">
    
    <!-- Section: FOR USERS -->
    <div class="section-label">FOR USERS</div>
    <ul class="nav-list">
      
      <!-- Expandable Item: Getting Started -->
      <li class="nav-item expanded">
        <div class="nav-link" onclick="toggleNav(this)">
          <span>Getting Started</span>
          <i class="fa-solid fa-chevron-down icon"></i>
        </div>
        <ul class="sub-nav">
          <li class="nav-item">
            <a href="#" class="nav-link active">Installation</a>
          </li>
          <li class="nav-item">
            <a href="#" class="nav-link">Build App</a>
          </li>
        </ul>
      </li>

      <!-- Standard Items -->
      <li class="nav-item"><a href="#" class="nav-link">Community</a></li>
      <li class="nav-item"><a href="#" class="nav-link">FAQ</a></li>
    </ul>

    <!-- Section: FOR DEVELOPERS -->
    <div class="section-label">FOR DEVELOPERS</div>
    <ul class="nav-list">
      
      <!-- Expandable Item: Developer Guide -->
      <li class="nav-item">
        <div class="nav-link" onclick="toggleNav(this)">
          <span>Developer Guide</span>
          <i class="fa-solid fa-chevron-down icon"></i>
        </div>
        <ul class="sub-nav">
          <li class="nav-item"><a href="#" class="nav-link">Architecture</a></li>
        </ul>
      </li>
      
    </ul>
  </div>

  <!-- Sidebar Footer: Project Switcher Dropdown -->
  <div class="sidebar-footer">
    <div class="project-switcher" id="switcher">
      <a href="https://holoviz.org" target="_blank" class="switcher-main">
        HoloViz.org
        <i class="fa-solid fa-arrow-up-right-from-square fa-external-link"></i>
      </a>
      <button class="switcher-toggle" id="dropdownBtn" aria-label="Toggle Project Switcher">
        <i class="fa-solid fa-caret-down"></i>
      </button>
      
      <!-- Dropdown Menu -->
      <ul class="dropdown-menu" id="dropdownMenu">
        <li><a class="dropdown-item" href="#">hvPlot</a></li>
        <li><a class="dropdown-item" href="#">HoloViews</a></li>
      </ul>
    </div>
  </div>
</aside>
```

### CSS (`sidebar.css`)
```css
/* CSS Variables based on PyData Sphinx Theme */
:root {
  --sidebar-bg: #ffffff;
  --sidebar-border: #e5e7eb;
  --text-main: #333333;
  --text-muted: #6b7280;
  --hover-bg: #f3f4f6;
  --active-text: #005b9f; /* Panel Blue */
  --dropdown-bg: #ffffff;
  --font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
}

/* Dark mode support */
@media (prefers-color-scheme: dark) {
  :root {
    --sidebar-bg: #1e1e21;
    --sidebar-border: #374151;
    --text-main: #e5e7eb;
    --text-muted: #9ca3af;
    --hover-bg: #374151;
    --active-text: #3b82f6;
    --dropdown-bg: #2d2d30;
  }
}

* { box-sizing: border-box; }

/* Mobile Hamburger Button */
.mobile-toggle {
  display: none;
  position: fixed;
  top: 1rem;
  left: 1rem;
  z-index: 100;
  background: var(--sidebar-bg);
  border: 1px solid var(--sidebar-border);
  color: var(--text-main);
  padding: 0.5rem 0.75rem;
  border-radius: 4px;
  cursor: pointer;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
.mobile-toggle:hover { background: var(--hover-bg); }

/* Sidebar Container */
.sidebar {
  width: 260px;
  background: var(--sidebar-bg);
  border-right: 1px solid var(--sidebar-border);
  height: 100vh;
  display: flex;
  flex-direction: column;
  position: fixed;
  left: 0;
  top: 0;
  transition: transform 0.3s ease;
  z-index: 50;
  font-family: var(--font-family);
  color: var(--text-main);
}

.sidebar-content {
  padding: 1.5rem 1rem;
  flex-grow: 1;
  overflow-y: auto;
}

/* Section Labels */
.section-label {
  font-size: 0.75rem;
  font-weight: 700;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 0.05em;
  margin: 1.5rem 0 0.5rem 0;
}
.section-label:first-child { margin-top: 0; }

/* Navigation List */
.nav-list { list-style: none; padding: 0; margin: 0; }
.nav-item { margin-bottom: 2px; }

/* Navigation Links */
.nav-link {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.4rem 0.5rem;
  color: var(--text-main);
  text-decoration: none;
  border-radius: 4px;
  font-size: 0.95rem;
  transition: background-color 0.2s, color 0.2s;
  cursor: pointer;
}
.nav-link:hover { background-color: var(--hover-bg); }
.nav-link.active {
  color: var(--active-text);
  font-weight: 600;
}
.nav-link .icon {
  font-size: 0.75rem;
  color: var(--text-muted);
  transition: transform 0.2s;
}

/* Expandable Items */
.nav-item.expanded > .nav-link .icon { transform: rotate(180deg); }
.sub-nav {
  display: none;
  list-style: none;
  margin-left: 1rem;
  border-left: 1px solid var(--sidebar-border);
  padding-left: 0.5rem;
  margin-top: 2px;
}
.nav-item.expanded > .sub-nav { display: block; }

/* Bottom Dropdown (Project Switcher) */
.sidebar-footer {
  padding: 1rem;
  border-top: 1px solid var(--sidebar-border);
  background: var(--sidebar-bg);
}

.project-switcher {
  position: relative;
  display: flex;
  width: 100%;
  border: 1px solid var(--sidebar-border);
  border-radius: 4px;
  background: var(--dropdown-bg);
}
.project-switcher:hover { border-color: var(--text-muted); }
.switcher-main {
  flex-grow: 1;
  padding: 0.5rem 0.75rem;
  color: var(--text-main);
  text-decoration: none;
  font-size: 0.9rem;
  font-weight: 500;
  border-right: 1px solid var(--sidebar-border);
}
.switcher-main:hover {
  color: var(--active-text);
  text-decoration: underline;
  text-decoration-thickness: 2px;
}
.switcher-main .fa-external-link {
  font-size: 0.75em;
  margin-left: 0.3em;
  color: var(--text-muted);
}
.switcher-toggle {
  background: none;
  border: none;
  padding: 0 0.75rem;
  cursor: pointer;
  color: var(--text-main);
}
.switcher-toggle:hover { background: var(--hover-bg); }

/* Dropdown Menu List */
.dropdown-menu {
  display: none;
  position: absolute;
  bottom: calc(100% + 5px);
  left: 0;
  width: 100%;
  background: var(--dropdown-bg);
  border: 1px solid var(--sidebar-border);
  border-radius: 4px;
  box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1);
  list-style: none;
  padding: 0.5rem 0;
  z-index: 10;
  margin: 0;
}
.dropdown-menu.show { display: block; }
.dropdown-item {
  display: block;
  padding: 0.4rem 1rem;
  color: var(--text-main);
  text-decoration: none;
  font-size: 0.85rem;
}
.dropdown-item:hover {
  background-color: var(--hover-bg);
  color: var(--active-text);
}

/* Mobile Responsive Styles */
@media (max-width: 768px) {
  .mobile-toggle { display: block; }
  .sidebar { transform: translateX(-100%); }
  .sidebar.open { transform: translateX(0); }
  
  .sidebar-overlay {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0,0,0,0.5);
    z-index: 40;
  }
  .sidebar-overlay.show { display: block; }
}
```

### JS (`sidebar.js`)
```javascript
// Expand/Collapse Navigation sub-menus
function toggleNav(element) {
  const parentLi = element.parentElement;
  parentLi.classList.toggle('expanded');
}

// Dropdown (Project Switcher) Logic
const dropdownBtn = document.getElementById('dropdownBtn');
const dropdownMenu = document.getElementById('dropdownMenu');

if (dropdownBtn && dropdownMenu) {
  dropdownBtn.addEventListener('click', (e) => {
    e.stopPropagation(); // Prevent clicking from immediately closing it
    dropdownMenu.classList.toggle('show');
  });

  // Close the dropdown when clicking outside of it
  document.addEventListener('click', (e) => {
    if (!dropdownBtn.contains(e.target) && !dropdownMenu.contains(e.target)) {
      dropdownMenu.classList.remove('show');
    }
  });
}

// Mobile Sidebar Toggle Logic
const mobileToggle = document.getElementById('mobileToggle');
const sidebar = document.getElementById('sidebar');
const overlay = document.getElementById('sidebarOverlay');

function toggleSidebar() {
  if (sidebar) sidebar.classList.toggle('open');
  if (overlay) overlay.classList.toggle('show');
}

if (mobileToggle) mobileToggle.addEventListener('click', toggleSidebar);
if (overlay) overlay.addEventListener('click', toggleSidebar);
```

## Customization Guide

### 1. Theming and Colors
All colors are managed by CSS variables at the top of the CSS file. To change the theme, update the `:root` pseudo-class:
- **Change the accent color (active link text)**: Modify `--active-text` (e.g., `#ff5722` for orange).
- **Modify the background**: Change `--sidebar-bg`.

### 2. Renaming Sections
To rename or add a section group, simply create a `<div>` with the `.section-label` class above a `.nav-list` `<ul>`:
```html
<div class="section-label">NEW SECTION</div>
<ul class="nav-list">...</ul>
```

### 3. Adding New Links
Add standard links directly inside a `.nav-list`:
```html
<li class="nav-item">
  <a href="/my-page" class="nav-link">My Page</a>
</li>
```
To set a link as active, add the `active` class to the `.nav-link`.

### 4. Modifying the Project Switcher
Inside the `.sidebar-footer`, look for `#dropdownMenu`. Add or remove `<li>` elements to change the sites in the dropdown. You can also add dividers:
```html
<li><hr class="dropdown-divider"></li>
```

## Integration Steps

### Dependencies
- **Font Awesome 6+**: Required for icons (`fa-bars`, `fa-chevron-down`, `fa-caret-down`, `fa-external-link`). Add this to your head: `<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">`
- **JS Frameworks**: None required natively (Vanilla JS/CSS).

### Plain HTML Site
1. Include the Font Awesome `<link>` tag in your `<head>`.
2. Add the CSS from `sidebar.css` into your existing stylesheet or `<style>` block.
3. Paste the HTML directly inside your `<body>`.
4. Include `sidebar.js` at the bottom of your page before `</body>`.
5. Ensure your main page content has `margin-left: 260px` applied on desktop screens to avoid overlapping the sidebar.

### React / Next.js
If you prefer a React Component over Vanilla HTML/JS, use this functional component structure:

```tsx
import React, { useState, useEffect, useRef } from 'react';
import './Sidebar.css'; // Make sure to paste the CSS here!

export default function Sidebar() {
  const [isMobileOpen, setIsMobileOpen] = useState(false);
  const [isDropdownOpen, setIsDropdownOpen] = useState(false);
  const [expandedNavs, setExpandedNavs] = useState({ gettingStarted: true });
  
  const dropdownRef = useRef(null);

  // Close dropdown on outside click
  useEffect(() => {
    function handleClickOutside(event) {
      if (dropdownRef.current && !dropdownRef.current.contains(event.target)) {
        setIsDropdownOpen(false);
      }
    }
    document.addEventListener("mousedown", handleClickOutside);
    return () => document.removeEventListener("mousedown", handleClickOutside);
  }, []);

  const toggleNav = (key) => {
    setExpandedNavs(prev => ({ ...prev, [key]: !prev[key] }));
  };

  return (
    <>
      <button className="mobile-toggle" onClick={() => setIsMobileOpen(true)}>
        <i className="fa-solid fa-bars"></i>
      </button>
      
      <div 
        className={`sidebar-overlay ${isMobileOpen ? 'show' : ''}`} 
        onClick={() => setIsMobileOpen(false)}
      />

      <aside className={`sidebar ${isMobileOpen ? 'open' : ''}`}>
        <div className="sidebar-content">
          <div className="section-label">FOR USERS</div>
          <ul className="nav-list">
            <li className={`nav-item ${expandedNavs.gettingStarted ? 'expanded' : ''}`}>
              <div className="nav-link" onClick={() => toggleNav('gettingStarted')}>
                <span>Getting Started</span>
                <i className="fa-solid fa-chevron-down icon"></i>
              </div>
              <ul className="sub-nav">
                <li className="nav-item"><a href="#" className="nav-link active">Installation</a></li>
              </ul>
            </li>
          </ul>
        </div>

        <div className="sidebar-footer">
          <div className="project-switcher" ref={dropdownRef}>
            <a href="https://holoviz.org" target="_blank" className="switcher-main">
              HoloViz.org <i className="fa-solid fa-arrow-up-right-from-square fa-external-link"></i>
            </a>
            <button className="switcher-toggle" onClick={() => setIsDropdownOpen(!isDropdownOpen)}>
              <i className="fa-solid fa-caret-down"></i>
            </button>
            
            {isDropdownOpen && (
              <ul className="dropdown-menu show">
                <li><a className="dropdown-item" href="#">hvPlot</a></li>
                <li><a className="dropdown-item" href="#">HoloViews</a></li>
              </ul>
            )}
          </div>
        </div>
      </aside>
    </>
  );
}
```
