[← Back to profile](../README.md)

# Atlas OS interface

**React 19 · TypeScript · Vite · Tailwind CSS v4 · TanStack Router and Query · Framer Motion · Recharts · PWA**

A custom dashboard interface for a human-performance platform. It shows live physiological and training data in a tactile, premium design, and I treated it as a design-systems project as well as an app.

## Design

- Asymmetric clipped panels, frosted glass surfaces with film-grain textures, and a cursor-driven light source that lights glass panels.
- Spring-driven motion: staggered reveals and hover lift, with motion values bound directly for smooth scrolling and dragging.
- A theme system with settings that flow through context, local storage and window events.

## Architecture

- Schema-driven layouts: routes are thin and render a feature from one declarative schema, which defines sidebars, header metrics, themes and widget lists.
- A snapping grid (40px units) for dragging and resizing widgets, with symmetric swaps on overlap and row compression so nothing jumps.
- A telemetry engine with generic chart templates that drop secondary detail when a widget gets small.
- A generator CLI for new components and widgets, installable as a PWA, and a database layer with mock fallbacks so it runs offline.
- Performance work: code splitting, production devtools stripped, canvas layout bounds cached.

## Direction

Turn the visual engine into a reusable UI library and make the database connection pluggable for other developers.
