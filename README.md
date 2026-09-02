# Nitro Velocity — Production Static Web Build

This package is a self-contained, dependency-free web application for the Nitro Velocity UI/gameplay simulator.

## Run locally
Open `index.html` directly in a modern browser, or serve the folder with any static web server.

## Deploy live
Upload the **contents of this folder** to a static host such as Vercel, Netlify, GitHub Pages, or any standard web server. No build command or environment variables are required.

## Included working features
- Driver profile creation/login validation with local session persistence
- Open-world hub navigation and mission selection
- Audi / Range Rover / Thar switching
- Live paint and rim customization with local autosave
- Steering, graphics, motion, audio, gameplay and police toggles
- Track selection
- Dynamic racing HUD, speed/RPM/gear simulation and Nitro Boost
- Police alert and manual Busted trigger
- Retry and Return to Hub loop
- Responsive desktop/mobile layout
- No external JS/CSS libraries, CDN dependencies, or broken internal links

## Important scope note
This is a production-ready **static web game/UI build** and simulator. It does not provide a real server-side authentication system, multiplayer backend, real cloud database, payments, or a full 3D game engine. The profile and progress state are persisted in browser localStorage.
