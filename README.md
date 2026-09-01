# Clock-Tick-Tock
Bruh its a clock I TOTALLY made this....
# Nature Clock

A lightweight, browser-based ambient clock interface built with vanilla HTML, CSS, and JavaScript.

## Overview

Nature Clock is a fullscreen digital clock designed around dynamic background video scenes, glassmorphism UI, smooth transitions, and minimal user interaction.

The application runs entirely client-side and does not require a backend or build system.

## Core Features

- Real-time 12-hour digital clock
- Live date display
- AM/PM indicator
- Animated seconds separator
- Automatic scene rotation
- Randomised scene ordering
- Manual scene selection
- Scene categories
- Background video Crossfading
- Scene looping
- Previous/next scene navigation
- Loading and failure handling
- Responsive mobile layout
- Reduced-motion accessibility support
- Glassmorphism interface
- Keyboard controls

## Scene System

Scenes are defined through a JavaScript configuration array.

Each scene contains:

- `name` — Display name
- `url` — Remote MP4 video source
- `category` — Menu grouping/category

Current categories include:

- Nature
- Night
- Cyberpunk
- Abstract

Scenes are initially shuffled using a Fisher-Yates-style randomisation algorithm, preventing the interface from always following the same sequence.

## Video Architecture

The application uses two HTML5 `<video>` elements:

- `videoA`
- `videoB`

The active video remains visible while the secondary element loads the next scene. Once the new source emits `canplay`, it becomes active and the previous video is paused.

This double-buffered approach prevents an unloaded or broken video from replacing the currently visible scene.

A 15-second safety timeout is also implemented. If a video fails to become playable within that window, the scene is treated as unavailable and the application attempts another scene.

## Clock Engine

The clock is driven by JavaScript's native `Date` API.

The update loop executes once per second and synchronises:

- Hours
- Minutes
- Seconds
- AM/PM
- Formatted calendar date

The interface only re-animates the hour and minute elements when their values actually change, reducing unnecessary DOM animation.

Numeric font features are enabled to maintain consistent digit width and prevent layout shifting.

## Interface

The visual layer uses:

- CSS custom properties
- Backdrop filtering
- Semi-transparent surfaces
- Radial gradients
- Vignette effects
- Drop shadows
- Animated opacity transitions
- Responsive media queries

The primary clock container uses a translucent glass surface with backdrop blur to separate the interface from the moving video background.

## Interaction

### Keyboard

`Space`  
Open or close the scene menu.

`Escape`  
Close the scene menu.

### Menu

The scene menu allows users to:

- Select a specific scene
- Enable scene looping
- Skip to the next scene

Selecting a scene also updates the internal shuffle position so subsequent navigation remains consistent with the current sequence.

## Error Handling

Video loading is deliberately fail-safe.

A failed scene does not replace the currently displayed video. Instead, the application:

1. Detects the loading failure.
2. Removes the invalid source.
3. Restores the loading state.
4. Attempts another scene.
5. Limits recursive retry attempts to prevent an infinite failure loop.

This ensures a broken remote asset does not leave the interface displaying an empty background.

## Accessibility

The application includes a `prefers-reduced-motion` media query.

When reduced motion is requested:

- Initial entrance animation is disabled.
- Digit pop animations are disabled.
- Video transitions are shortened.

This allows users with motion sensitivity to use the interface with reduced visual movement.

## Dependencies

The project uses no JavaScript frameworks or external runtime libraries.

External resources are limited to:

- Google Fonts
- Pexels-hosted MP4 video assets

Primary fonts:

- Orbitron
- Manrope

## Technology Stack

```text
HTML5
CSS3
JavaScript (ES6+)
HTML5 Video API
Date API
DOM API
CSS Backdrop Filter
CSS Media Queries
```

## File Structure

```text
nature-clock.html
```

The project is currently self-contained in a single HTML document containing:

```text
HTML
 ├── Interface markup
 ├── Video containers
 ├── Scene menu
 └── Clock display

CSS
 ├── Theme variables
 ├── Glass UI
 ├── Animations
 ├── Responsive layout
 └── Accessibility rules

JavaScript
 ├── Scene configuration
 ├── Shuffle engine
 ├── Video management
 ├── Menu controller
 ├── Keyboard interaction
 └── Clock synchronisation
```

## Running

No installation or compilation is required.

Open `nature-clock.html` in a modern web browser with an active internet connection.

Because the background scenes are remotely hosted MP4 files, video playback depends on network connectivity and the availability of the configured remote assets.

## Design Philosophy

The implementation intentionally avoids frameworks and unnecessary dependencies. The result is a compact client-side application where the presentation layer, state management, media handling, and clock logic are all directly observable within a single source file.

The architecture prioritises visual smoothness, graceful media failure, minimal DOM manipulation, and low deployment complexity.
README.md
Displaying README.md.
