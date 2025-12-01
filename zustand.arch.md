# hl_overview

High level overview of the codebase

# Repository Analysis: Zustand

## 0. Repository Name
[[zustand]]

## 1. Project Purpose

**Zustand** is a lightweight, fast, and scalable state management solution for React applications. It solves the problem of managing application state without the boilerplate and complexity of larger solutions like Redux.

**Primary Domain:** Frontend state management library for React/JavaScript applications.

**Key Features:**
- Minimal API surface with hooks-based approach
- Framework-agnostic core (vanilla JS) with React bindings
- Built-in middleware support (persist, devtools, immer, redux-style reducers)
- TypeScript support
- SSR compatibility

## 2. Architecture Pattern

**Library/Package Architecture** with a **Middleware Pattern**:
- Core vanilla store implementation
- Framework-specific bindings (React)
- Composable middleware system for extending functionality
- Separation between core logic and React integration

## 3. Technology Stack

### Primary Languages
- **TypeScript** - Main development language
- **JavaScript/JSX** - Examples and demo applications

### Build & Development Tools
| Tool | Purpose |
|------|---------|
| Rollup | Module bundler (`rollup.config.mjs`) |
| Vitest | Testing framework (`vitest.config.mts`) |
| pnpm | Package manager (`pnpm-lock.yaml`, `pnpm-workspace.yaml`) |
| ESLint | Linting (`eslint.config.mjs`) |
| Prettier | Code formatting (`.prettierignore`) |
| TypeScript | Type checking (`tsconfig.json`) |

### Dependencies (from package.json context)
- **React** - Target framework for bindings
- **Immer** - Immutable state updates (middleware)
- **Vite** - Used in examples for development

### Testing
- Vitest for unit/integration tests
- Multiple test configurations for different TypeScript versions and build targets

## 4. Initial Structure Impression

| Component | Description |
|-----------|-------------|
| `src/` | Core library source code |
| `tests/` | Test suites |
| `docs/` | Documentation files |
| `examples/` | Demo applications (demo + starter) |
| `.github/` | CI/CD workflows and templates |

This is a **monorepo-style library project** focused on publishing an npm package with comprehensive documentation and examples.

## 5. Configuration/Package Files

```
Root Configuration:
├── package.json           # Main package configuration
├── pnpm-lock.yaml         # Dependency lock file
├── pnpm-workspace.yaml    # Monorepo workspace config
├── tsconfig.json          # TypeScript configuration
├── rollup.config.mjs      # Build configuration
├── vitest.config.mts      # Test configuration
├── eslint.config.mjs      # Linting rules
├── .prettierignore        # Formatter ignore patterns
├── .gitignore             # Git ignore patterns
├── LICENSE                # MIT License
├── FUNDING.json           # Funding information
└── CONTRIBUTING.md        # Contribution guidelines

Examples:
├── examples/demo/package.json
├── examples/demo/vite.config.js
├── examples/starter/package.json
├── examples/starter/vite.config.ts
└── examples/starter/tsconfig.json

CI/CD:
└── .github/workflows/*.yml  # Multiple workflow files
```

## 6. Directory Structure

### Source Code (`src/`)
```
src/
├── index.ts              # Main entry point, re-exports
├── vanilla.ts            # Framework-agnostic store implementation
├── react.ts              # React hooks and bindings
├── shallow.ts            # Shallow comparison utilities
├── traditional.ts        # Traditional API (legacy support)
├── types.d.ts            # Type declarations
├── middleware.ts         # Middleware re-exports
├── middleware/           # Individual middleware implementations
│   ├── combine.ts        # State combining middleware
│   ├── devtools.ts       # Redux DevTools integration
│   ├── immer.ts          # Immer integration
│   ├── persist.ts        # State persistence
│   ├── redux.ts          # Redux-style reducer pattern
│   ├── subscribeWithSelector.ts  # Selective subscriptions
│   └── ssrSafe.ts        # SSR safety utilities
├── vanilla/
│   └── shallow.ts        # Vanilla shallow utilities
└── react/
    └── shallow.ts        # React shallow utilities
```

**Organization Pattern:** Organized by **layer/concern**:
- Core (vanilla) → React bindings → Middleware extensions

### Tests (`tests/`)
```
tests/
├── basic.test.tsx        # Core functionality tests
├── subscribe.test.tsx    # Subscription tests
├── shallow.test.tsx      # Shallow comparison tests
├── persistAsync.test.tsx # Async persistence tests
├── persistSync.test.tsx  # Sync persistence tests
├── devtools.test.tsx     # DevTools middleware tests
├── middlewareTypes.test.tsx  # Middleware typing tests
├── types.test.tsx        # TypeScript type tests
├── ssr.test.tsx          # Server-side rendering tests
├── setup.ts              # Test setup
├── test-utils.ts         # Test utilities
└── vanilla/              # Vanilla-specific tests
```

### Documentation (`docs/`)
```
docs/
├── getting-started/      # Introduction, comparisons
├── guides/               # Usage guides (TypeScript, testing, patterns)
├── apis/                 # API documentation
├── middlewares/          # Middleware documentation
├── hooks/                # React hooks documentation
├── integrations/         # Third-party integrations
├── migrations/           # Version migration guides
└── previous-versions/    # Legacy documentation
```

### Examples (`examples/`)
- **demo/** - Full-featured 3D demo application with Three.js
- **starter/** - Minimal starter template for new projects

## 7. High-Level Architecture

### Pattern: **Layered Library Architecture with Middleware Pipeline**

```
┌─────────────────────────────────────────────────────┐
│                   Consumer Layer                     │
│              (React Components/Hooks)                │
├─────────────────────────────────────────────────────┤
│                   React Bindings                     │
│     (useStore, useStoreWithEqualityFn, useShallow)  │
├─────────────────────────────────────────────────────┤
│                  Middleware Layer                    │
│  (persist, devtools, immer, redux, combine, etc.)   │
├─────────────────────────────────────────────────────┤
│                 Vanilla Core Store                   │
│        (createStore, subscribe, getState)            │
└─────────────────────────────────────────────────────┘
```

### Evidence Supporting This Architecture:

1. **Separation of Concerns:**
   - `vanilla.ts` - Pure JavaScript store (no React dependency)
   - `react.ts` - React-specific bindings
   - Middleware in separate modules

2. **Middleware Pattern:**
   - `src/middleware/` directory with composable enhancers
   - Each middleware wraps the store creator

3. **Observable/Subscription Pattern:**
   - `subscribe.test.tsx` tests
   - `subscribeWithSelector.ts` middleware

4. **Hooks-Based API:**
   - `docs/hooks/` documentation
   - `useStore`, `useShallow` exports

## 8. Build, Execution and Test

### Build Process
```bash
# Build using Rollup (produces multiple formats: ESM, CJS, UMD)
pnpm build  # Likely defined in package.json scripts
```

**Build Configuration:** `rollup.config.mjs` handles bundling with likely outputs:
- ES Modules (`esm`)
- CommonJS (`cjs`)
- TypeScript declarations

### Testing
```bash
# Run tests with Vitest
pnpm test

# Test configurations available:
# - Standard tests
# - Multiple TypeScript versions (.github/workflows/test-old-typescript.yml)
# - Multiple build formats (.github/workflows/test-multiple-builds.yml)
# - Multiple React/library versions (.github/workflows/test-multiple-versions.yml)
```

**Test Setup:** `tests/setup.ts` and `tests/test-utils.ts`

### Main Entry Points
```typescript
// Primary entry
src/index.ts  → exports create, createStore, useStore

// Vanilla (framework-agnostic)
src/vanilla.ts → exports createStore

// React bindings
src/react.ts → exports create, useStore

// Middleware
src/middleware.ts → exports all middleware
```

### CI/CD Workflows
| Workflow | Purpose |
|----------|---------|
| `test.yml` | Main test suite |
| `test-multiple-versions.yml` | Compatibility testing |
| `test-old-typescript.yml` | TypeScript version compatibility |
| `publish.yml` | NPM publishing |
| `preview-release.yml` | Preview releases |
| `docs.yml` | Documentation deployment |
| `compressed-size.yml` | Bundle size tracking |

### Running Examples
```bash
# Demo application
cd examples/demo
pnpm install
pnpm dev

# Starter template
cd examples/starter
pnpm install
pnpm dev
```

# module_deep_dive

Deep dive into modules

# Detailed Component Breakdown

## 📁 `src/` - Core Library Source

### 1. `src/index.ts`

**Core Responsibility:**
Main entry point that re-exports the primary Zustand API, providing the default export for library consumers.

**Key Components:**
- Re-exports from `./react` module
- Exposes the main `create` function and React-specific APIs

**Dependencies & Interactions:**
- Internal: Depends on `./react.ts`
- External: None directly

---

### 2. `src/vanilla.ts`

**Core Responsibility:**
Framework-agnostic state management core. Implements the fundamental store creation logic without any React dependencies.

**Key Components:**
- `createStore` function - Creates a vanilla JavaScript store
- State getter/setter logic
- Subscription management system
- `StoreApi` interface implementation

**Dependencies & Interactions:**
- Internal: None (this is the foundational module)
- External: None - pure JavaScript implementation

---

### 3. `src/react.ts`

**Core Responsibility:**
React bindings for Zustand, providing hooks-based API for React applications to consume stores.

**Key Components:**
- `create` function - Main store creation with React hooks
- `useStore` hook - Connects React components to stores
- Selector pattern implementation
- Re-rendering optimization logic

**Dependencies & Interactions:**
- Internal: `./vanilla.ts` for core store logic
- External: React (hooks API - `useSyncExternalStore`, `useRef`, `useCallback`)

---

### 4. `src/shallow.ts`

**Core Responsibility:**
Provides shallow comparison utilities for optimizing re-renders by comparing state slices.

**Key Components:**
- `shallow` function - Performs shallow equality comparison
- Export gateway for shallow comparison utilities

**Dependencies & Interactions:**
- Internal: `./vanilla/shallow.ts`
- External: None

---

### 5. `src/traditional.ts`

**Core Responsibility:**
Provides backward-compatible APIs and traditional patterns for users migrating from older versions or preferring different patterns.

**Key Components:**
- `createWithEqualityFn` - Store creation with custom equality function
- `useStoreWithEqualityFn` - Hook with custom comparison

**Dependencies & Interactions:**
- Internal: `./vanilla.ts`
- External: React

---

### 6. `src/middleware.ts`

**Core Responsibility:**
Barrel file that re-exports all middleware modules for convenient importing.

**Key Components:**
- Re-exports from `./middleware/*` modules

**Dependencies & Interactions:**
- Internal: All middleware modules
- External: None directly

---

### 7. `src/types.d.ts`

**Core Responsibility:**
TypeScript type declarations providing type safety and IDE support for the library.

**Key Components:**
- Store type definitions
- State type generics
- Middleware type utilities
- API interface declarations

**Dependencies & Interactions:**
- Internal: Referenced by all TypeScript modules
- External: None

---

## 📁 `src/middleware/` - Middleware Implementations

### 8. `src/middleware/combine.ts`

**Core Responsibility:**
Middleware for combining multiple state slices into a single store, enabling modular state organization.

**Key Components:**
- `combine` function - Merges initial state with actions/computed values
- Type inference utilities for combined states

**Dependencies & Interactions:**
- Internal: Core store types from `../vanilla.ts`
- External: None

---

### 9. `src/middleware/devtools.ts`

**Core Responsibility:**
Integration with Redux DevTools browser extension for debugging, time-travel, and state inspection.

**Key Components:**
- `devtools` middleware wrapper
- Connection management to DevTools extension
- Action logging and state serialization
- Time-travel debugging support

**Dependencies & Interactions:**
- Internal: `../vanilla.ts` for store API
- External: **Redux DevTools Extension API** (browser extension)

---

### 10. `src/middleware/immer.ts`

**Core Responsibility:**
Enables immutable state updates using mutable syntax through Immer library integration.

**Key Components:**
- `immer` middleware wrapper
- Draft state handling
- Produce function integration

**Dependencies & Interactions:**
- Internal: `../vanilla.ts`
- External: **Immer library** (peer dependency)

---

### 11. `src/middleware/persist.ts`

**Core Responsibility:**
State persistence middleware for saving and restoring state to/from storage (localStorage, sessionStorage, etc.).

**Key Components:**
- `persist` middleware function
- `PersistOptions` configuration interface
- Storage engine abstraction
- Hydration/rehydration logic
- Migration utilities for schema changes
- `createJSONStorage` helper

**Dependencies & Interactions:**
- Internal: `../vanilla.ts`
- External: **Storage APIs** (localStorage, sessionStorage, AsyncStorage, or custom)

---

### 12. `src/middleware/redux.ts`

**Core Responsibility:**
Redux-style reducer pattern middleware, allowing Redux-like action/reducer patterns within Zustand.

**Key Components:**
- `redux` middleware function
- `dispatch` function implementation
- Reducer pattern integration
- Action type handling

**Dependencies & Interactions:**
- Internal: `../vanilla.ts`
- External: None (implements Redux patterns without Redux dependency)

---

### 13. `src/middleware/subscribeWithSelector.ts`

**Core Responsibility:**
Enhanced subscription middleware allowing subscribers to listen to specific state slices with selectors.

**Key Components:**
- `subscribeWithSelector` middleware
- Selector-based subscription logic
- Equality function support for subscriptions

**Dependencies & Interactions:**
- Internal: `../vanilla.ts`
- External: None

---

### 14. `src/middleware/ssrSafe.ts`

**Core Responsibility:**
Server-side rendering safety utilities to prevent hydration mismatches and handle SSR environments.

**Key Components:**
- SSR detection utilities
- Safe initialization patterns
- Hydration handling

**Dependencies & Interactions:**
- Internal: `../vanilla.ts`
- External: None (handles SSR environment detection)

---

## 📁 `src/vanilla/` - Vanilla JavaScript Utilities

### 15. `src/vanilla/shallow.ts`

**Core Responsibility:**
Core shallow comparison implementation without React dependencies.

**Key Components:**
- `shallow` function - Object/array shallow equality comparison
- Type-safe comparison logic
- Handles edge cases (null, undefined, primitives)

**Dependencies & Interactions:**
- Internal: None (standalone utility)
- External: None

---

## 📁 `src/react/` - React-Specific Utilities

### 16. `src/react/shallow.ts`

**Core Responsibility:**
React-specific shallow comparison hook for use with selectors in React components.

**Key Components:**
- `useShallow` hook - Memoized shallow comparison for selectors
- Integration with React's rendering cycle

**Dependencies & Interactions:**
- Internal: `../vanilla/shallow.ts`
- External: React (hooks API)

---

## 📁 `tests/` - Test Suite

### 17. `tests/` (Main Test Directory)

**Core Responsibility:**
Comprehensive test suite validating all library functionality.

**Key Components:**
| File | Role |
|------|------|
| `basic.test.tsx` | Core store creation and usage tests |
| `devtools.test.tsx` | DevTools middleware integration tests |
| `middlewareTypes.test.tsx` | TypeScript middleware type tests |
| `persistAsync.test.tsx` | Async persistence tests |
| `persistSync.test.tsx` | Sync persistence tests |
| `setup.ts` | Test environment configuration |
| `shallow.test.tsx` | Shallow comparison tests |
| `ssr.test.tsx` | Server-side rendering tests |
| `subscribe.test.tsx` | Subscription system tests |
| `test-utils.ts` | Shared testing utilities |
| `types.test.tsx` | TypeScript type validation tests |

**Dependencies & Interactions:**
- Internal: All `src/` modules
- External: **Vitest** (test framework), **React Testing Library**

---

### 18. `tests/vanilla/`

**Core Responsibility:**
Tests specifically for vanilla (non-React) functionality.

**Key Components:**
| File | Role |
|------|------|
| `basic.test.ts` | Vanilla store tests |
| `shallow.test.tsx` | Vanilla shallow comparison tests |
| `subscribe.test.tsx` | Vanilla subscription tests |

**Dependencies & Interactions:**
- Internal: `src/vanilla.ts`, `src/vanilla/shallow.ts`
- External: **Vitest**

---

## 📁 `examples/` - Example Applications

### 19. `examples/demo/`

**Core Responsibility:**
Full-featured demo application showcasing Zustand capabilities in a real-world scenario.

**Key Components:**
| Directory/File | Role |
|----------------|------|
| `src/components/` | React UI components |
| `src/materials/` | Material/styling resources |
| `src/resources/` | Static resources and data |
| `src/utils/` | Utility functions |
| `vite.config.js` | Vite build configuration |

**Dependencies & Interactions:**
- Internal: Uses Zustand library
- External: **React**, **Vite**

---

### 20. `examples/starter/`

**Core Responsibility:**
Minimal starter template for new Zustand projects.

**Key Components:**
| File | Role |
|------|------|
| `src/` | Basic React app with Zustand |
| `vite.config.ts` | TypeScript Vite configuration |
| `tsconfig.json` | TypeScript configuration |

**Dependencies & Interactions:**
- Internal: Uses Zustand library
- External: **React**, **Vite**, **TypeScript**

---

## 📁 `docs/` - Documentation

### 21. `docs/` (Documentation Root)

**Core Responsibility:**
Comprehensive documentation for library users.

**Key Components:**
| Directory | Content |
|-----------|---------|
| `apis/` | API reference documentation |
| `middlewares/` | Middleware usage guides |
| `integrations/` | Third-party integration guides |
| `getting-started/` | Introduction and comparison docs |
| `guides/` | How-to guides and best practices |
| `hooks/` | React hooks documentation |
| `migrations/` | Version migration guides |
| `previous-versions/` | Legacy API documentation |

**Dependencies & Interactions:**
- Internal: References all library features
- External: None (static documentation)

---

## 📁 `.github/` - GitHub Configuration

### 22. `.github/workflows/`

**Core Responsibility:**
CI/CD automation for testing, building, and publishing.

**Key Components:**
| Workflow | Purpose |
|----------|---------|
| `test.yml` | Main test suite execution |
| `publish.yml` | NPM package publishing |
| `preview-release.yml` | Pre-release builds |
| `compressed-size.yml` | Bundle size monitoring |
| `docs.yml` | Documentation deployment |
| `test-multiple-builds.yml` | Cross-environment testing |
| `test-multiple-versions.yml` | Version compatibility testing |
| `test-old-typescript.yml` | TypeScript backwards compatibility |

**Dependencies & Interactions:**
- Internal: All project files
- External: **GitHub Actions**, **NPM Registry**

# dependencies

Analyze dependencies and external libraries

# Dependency and Architecture Analysis

## Repository: zustand_60c5b6ba

---

## Internal Modules

Based on the repository structure and source code organization, the following internal modules have been identified:

### Core Library (`/src/`)

| Module | File(s) | Description |
|--------|---------|-------------|
| **index** | `index.ts` | Main entry point that exports the public API of the zustand library |
| **react** | `react.ts` | React-specific bindings and hooks for state management integration with React components |
| **vanilla** | `vanilla.ts` | Framework-agnostic core store implementation that works without React |
| **shallow** | `shallow.ts` | Utility for shallow equality comparison, used to optimize re-renders |
| **traditional** | `traditional.ts` | Traditional/legacy API support for backwards compatibility |
| **middleware** | `middleware.ts` | Aggregated middleware exports for extending store functionality |
| **types** | `types.d.ts` | TypeScript type definitions for the library |

### Middleware Submodule (`/src/middleware/`)

| Module | File | Description |
|--------|------|-------------|
| **combine** | `combine.ts` | Middleware for combining multiple store slices into a single store |
| **devtools** | `devtools.ts` | Integration with Redux DevTools for debugging state changes |
| **immer** | `immer.ts` | Middleware enabling Immer-based immutable state updates |
| **persist** | `persist.ts` | Middleware for persisting store state to storage (localStorage, etc.) |
| **redux** | `redux.ts` | Middleware for Redux-style reducer pattern support |
| **ssrSafe** | `ssrSafe.ts` | Middleware for safe server-side rendering handling |
| **subscribeWithSelector** | `subscribeWithSelector.ts` | Middleware enabling selective subscription to specific state slices |

### Vanilla Submodule (`/src/vanilla/`)

| Module | File | Description |
|--------|------|-------------|
| **shallow** | `shallow.ts` | Vanilla (non-React) implementation of shallow comparison utilities |

### React Submodule (`/src/react/`)

| Module | File | Description |
|--------|------|-------------|
| **shallow** | `shallow.ts` | React-specific shallow comparison hook implementation |

---

## External Dependencies

### Production Dependencies

#### Main Library (`/package.json` - Peer Dependencies)

| Dependency | Official Name | Purpose |
|------------|---------------|---------|
| `react` | React | UI framework; core peer dependency for React bindings |
| `@types/react` | React Types | TypeScript type definitions for React |
| `immer` | Immer | Library for working with immutable state via the immer middleware |
| `use-sync-external-store` | use-sync-external-store | React hook for subscribing to external stores (React 18+ concurrent features support) |

#### Demo Example (`/examples/demo/package.json`)

| Dependency | Official Name | Purpose |
|------------|---------------|---------|
| `react` | React | UI framework for building the demo application |
| `react-dom` | React DOM | React package for DOM rendering |
| `zustand` | Zustand | The state management library (self-reference for demo) |
| `three` | Three.js | 3D graphics library for WebGL rendering |
| `@react-three/fiber` | React Three Fiber | React renderer for Three.js |
| `@react-three/drei` | Drei | Helper components and hooks for React Three Fiber |
| `@react-three/postprocessing` | React Three Postprocessing | Post-processing effects for React Three Fiber |
| `@types/three` | Three.js Types | TypeScript type definitions for Three.js |
| `meshline` | MeshLine | Library for drawing lines with thickness in Three.js |
| `postprocessing` | Postprocessing | Post-processing effects library for Three.js |
| `prism-react-renderer` | Prism React Renderer | Syntax highlighting component for React |
| `prismjs` | Prism | Syntax highlighting library |

#### Starter Example (`/examples/starter/package.json`)

| Dependency | Official Name | Purpose |
|------------|---------------|---------|
| `react` | React | UI framework |
| `react-dom` | React DOM | React package for DOM rendering |
| `zustand` | Zustand | The state management library (self-reference for starter) |

---

### Developer Dependencies

#### Main Library (`/package.json` - devDependencies)

| Dependency | Official Name | Purpose |
|------------|---------------|---------|
| `@eslint/js` | ESLint JS | ESLint's JavaScript configuration |
| `@redux-devtools/extension` | Redux DevTools Extension | Browser extension integration for debugging |
| `@rollup/plugin-alias` | Rollup Alias Plugin | Rollup plugin for module aliasing |
| `@rollup/plugin-node-resolve` | Rollup Node Resolve | Rollup plugin for resolving node_modules |
| `@rollup/plugin-replace` | Rollup Replace Plugin | Rollup plugin for replacing strings during build |
| `@rollup/plugin-typescript` | Rollup TypeScript Plugin | Rollup plugin for TypeScript compilation |
| `@testing-library/jest-dom` | Testing Library Jest DOM | Custom Jest matchers for DOM testing |
| `@testing-library/react` | Testing Library React | React testing utilities |
| `@types/node` | Node.js Types | TypeScript type definitions for Node.js |
| `@types/react` | React Types | TypeScript type definitions for React |
| `@types/react-dom` | React DOM Types | TypeScript type definitions for React DOM |
| `@types/use-sync-external-store` | use-sync-external-store Types | TypeScript type definitions for use-sync-external-store |
| `@vitest/coverage-v8` | Vitest Coverage V8 | Code coverage provider for Vitest |
| `@vitest/eslint-plugin` | Vitest ESLint Plugin | ESLint plugin for Vitest |
| `@vitest/ui` | Vitest UI | UI interface for Vitest test runner |
| `esbuild` | esbuild | Fast JavaScript/TypeScript bundler |
| `eslint` | ESLint | JavaScript/TypeScript linter |
| `eslint-import-resolver-typescript` | ESLint Import Resolver TypeScript | TypeScript import resolution for ESLint |
| `eslint-plugin-import` | ESLint Plugin Import | ESLint plugin for import/export syntax |
| `eslint-plugin-jest-dom` | ESLint Plugin Jest DOM | ESLint plugin for jest-dom |
| `eslint-plugin-react` | ESLint Plugin React | ESLint plugin for React |
| `eslint-plugin-react-hooks` | ESLint Plugin React Hooks | ESLint plugin for React Hooks rules |
| `eslint-plugin-testing-library` | ESLint Plugin Testing Library | ESLint plugin for Testing Library |
| `immer` | Immer | Immutable state library (dev testing of immer middleware) |
| `jsdom` | jsdom | DOM implementation for Node.js (testing environment) |
| `json` | json | JSON CLI tool |
| `prettier` | Prettier | Code formatter |
| `react` | React | UI framework (dev testing) |
| `react-dom` | React DOM | React DOM rendering (dev testing) |
| `redux` | Redux | State management library (dev testing of redux middleware) |
| `rollup` | Rollup | Module bundler |
| `rollup-plugin-esbuild` | Rollup Plugin esbuild | Rollup plugin using esbuild for transformation |
| `shelljs` | ShellJS | Unix shell commands for Node.js |
| `shx` | shx | Cross-platform shell commands |
| `tslib` | tslib | TypeScript runtime helpers |
| `typescript` | TypeScript | TypeScript compiler |
| `typescript-eslint` | TypeScript ESLint | TypeScript support for ESLint |
| `use-sync-external-store` | use-sync-external-store | React external store hook (dev testing) |
| `vitest` | Vitest | Unit testing framework |

#### Demo Example (`/examples/demo/package.json` - devDependencies)

| Dependency | Official Name | Purpose |
|------------|---------------|---------|
| `@eslint/js` | ESLint JS | ESLint's JavaScript configuration |
| `@types/react` | React Types | TypeScript type definitions for React |
| `@types/react-dom` | React DOM Types | TypeScript type definitions for React DOM |
| `@vitejs/plugin-react-swc` | Vite React SWC Plugin | Vite plugin for React with SWC compiler |
| `eslint` | ESLint | JavaScript linter |
| `eslint-plugin-react` | ESLint Plugin React | ESLint plugin for React |
| `eslint-plugin-react-hooks` | ESLint Plugin React Hooks | ESLint plugin for React Hooks |
| `eslint-plugin-react-refresh` | ESLint Plugin React Refresh | ESLint plugin for React Refresh |
| `globals` | globals | Global identifiers for ESLint |
| `vite` | Vite | Frontend build tool and dev server |

#### Starter Example (`/examples/starter/package.json` - devDependencies)

| Dependency | Official Name | Purpose |
|------------|---------------|---------|
| `@types/react` | React Types | TypeScript type definitions for React |
| `@types/react-dom` | React DOM Types | TypeScript type definitions for React DOM |
| `@vitejs/plugin-react-swc` | Vite React SWC Plugin | Vite plugin for React with SWC compiler |
| `typescript` | TypeScript | TypeScript compiler |
| `vite` | Vite | Frontend build tool and dev server |

# core_entities

Core entities and their relationships

# Domain Model Analysis: Zustand State Management Library

## Overview

This repository is **Zustand**, a lightweight state management library for React. The domain models revolve around **state management primitives** rather than traditional business entities. The core abstractions deal with stores, state, actions, subscriptions, and middleware.

---

## 1. Common Data Entities / Domain Models

### 1.1 **Store**
The central entity representing a state container.

### 1.2 **State**
The actual data held within a store at any given time.

### 1.3 **StateCreator / StoreInitializer**
A function or configuration that defines how state and actions are created.

### 1.4 **Listener / Subscription**
Represents observers subscribed to state changes.

### 1.5 **Middleware**
Enhancers that wrap store creation to add functionality.

### 1.6 **Selector**
Functions that extract specific slices of state.

### 1.7 **PersistConfig / Storage**
Configuration for persisting state across sessions.

---

## 2. Key Attributes / Fields

### **Store (StoreApi)**
| Attribute | Type | Description |
|-----------|------|-------------|
| `getState` | `() => T` | Returns current state snapshot |
| `setState` | `(partial, replace?) => void` | Updates state (partial or full replace) |
| `subscribe` | `(listener) => unsubscribe` | Registers a listener for state changes |
| `getInitialState` | `() => T` | Returns the initial state value |
| `destroy` | `() => void` | Cleans up the store (optional) |

### **State (Generic `T`)**
| Attribute | Type | Description |
|-----------|------|-------------|
| `[key]` | `any` | User-defined state properties |
| `actions` | `Functions` | Typically embedded action methods that call `setState` |

### **Listener**
| Attribute | Type | Description |
|-----------|------|-------------|
| `callback` | `(state: T, prevState: T) => void` | Function called on state change |
| `selector` | `(state: T) => U` | Optional selector for fine-grained subscriptions |
| `equalityFn` | `(a, b) => boolean` | Custom equality check (e.g., `shallow`) |

### **Middleware**
| Attribute | Type | Description |
|-----------|------|-------------|
| `name` | `string` | Middleware identifier (e.g., `'persist'`, `'devtools'`) |
| `wrapper` | `(storeCreator) => storeCreator` | Higher-order function wrapping store creation |

### **PersistOptions**
| Attribute | Type | Description |
|-----------|------|-------------|
| `name` | `string` | Unique storage key identifier |
| `storage` | `StateStorage` | Storage adapter (localStorage, sessionStorage, async) |
| `partialize` | `(state) => partial` | Select which state to persist |
| `onRehydrateStorage` | `(state) => void` | Callback when state is restored |
| `version` | `number` | Schema version for migrations |
| `migrate` | `(persisted, version) => state` | Migration function between versions |
| `merge` | `(persisted, current) => state` | Custom merge strategy |
| `skipHydration` | `boolean` | Defer hydration for SSR |

### **DevtoolsOptions**
| Attribute | Type | Description |
|-----------|------|-------------|
| `name` | `string` | Store name in Redux DevTools |
| `enabled` | `boolean` | Toggle devtools connection |
| `anonymousActionType` | `string` | Default action name |
| `store` | `string` | Store identifier for multiple stores |

### **Shallow Comparison Result**
| Attribute | Type | Description |
|-----------|------|-------------|
| `objA` | `T` | First object to compare |
| `objB` | `T` | Second object to compare |
| `result` | `boolean` | Whether objects are shallowly equal |

---

## 3. Entity Relationships

```
┌─────────────────────────────────────────────────────────────────────────┐
│                          ZUSTAND DOMAIN MODEL                           │
└─────────────────────────────────────────────────────────────────────────┘

                              ┌──────────────┐
                              │ StateCreator │
                              │  (Function)  │
                              └──────┬───────┘
                                     │ creates
                                     ▼
┌──────────────┐   wraps    ┌──────────────┐   produces   ┌───────────┐
│  Middleware  │──────────▶ │    Store     │ ───────────▶ │   State   │
│  (1 to Many) │            │  (StoreApi)  │              │    (T)    │
└──────────────┘            └──────┬───────┘              └───────────┘
       │                           │                            ▲
       │                           │ has many                   │
       │                           ▼                            │
       │                    ┌──────────────┐                    │
       │                    │  Listener/   │   observes         │
       │                    │ Subscription │────────────────────┘
       │                    └──────┬───────┘
       │                           │ uses
       │                           ▼
       │                    ┌──────────────┐
       │                    │   Selector   │
       │                    │  (Function)  │
       │                    └──────────────┘
       │
       │ types of middleware
       ▼
┌─────────────────────────────────────────────────────┐
│                   MIDDLEWARE TYPES                  │
├─────────────┬─────────────┬─────────────┬──────────┤
│   persist   │  devtools   │   immer     │  redux   │
├─────────────┼─────────────┼─────────────┼──────────┤
│  combine    │ subscribeWithSelector     │ ssrSafe  │
└─────────────┴─────────────┴─────────────┴──────────┘
       │
       │ persist middleware uses
       ▼
┌──────────────────┐         ┌──────────────────┐
│  PersistConfig   │────────▶│  StateStorage    │
│                  │  uses   │  (Adapter)       │
└──────────────────┘         └──────────────────┘
```

---

## 4. Relationship Descriptions

| Relationship | Type | Description |
|--------------|------|-------------|
| **Store → State** | One-to-One | Each store holds exactly one state object at a time |
| **Store → Listener** | One-to-Many | A store can have multiple subscribers |
| **Listener → Selector** | One-to-One (Optional) | A listener may use a selector for targeted updates |
| **Middleware → Store** | Many-to-One (Composition) | Multiple middlewares compose to wrap a single store |
| **PersistMiddleware → Storage** | One-to-One | Persist config binds to one storage adapter |
| **StateCreator → Store** | One-to-One | A creator function produces one store instance |
| **Store → EqualityFn** | One-to-One (Optional) | Stores can use custom equality for `useStore` hooks |

---

## 5. Key Patterns Identified

### **Middleware Chain Pattern**
```
combine → devtools → persist → subscribeWithSelector → immer → baseStore
```
Middlewares wrap each other, each enhancing the store API.

### **Selector + Equality Pattern**
```typescript
// Selector extracts slice, equalityFn prevents unnecessary rerenders
useStore(
  (state) => state.user,      // Selector
  shallow                      // EqualityFn
)
```

### **React Hook Binding**
```
Vanilla Store (StoreApi) ──▶ useSyncExternalStore ──▶ React Hook (useStore)
```

---

## 6. Summary Table

| Entity | Purpose | Key Relationships |
|--------|---------|-------------------|
| **Store** | State container with API | Holds State, has Listeners |
| **State** | Application data | Owned by Store |
| **StateCreator** | Factory for state + actions | Creates Store |
| **Listener** | Observer callback | Subscribes to Store |
| **Selector** | State slice extractor | Used by Listeners/Hooks |
| **Middleware** | Store enhancer | Wraps Store creation |
| **PersistConfig** | Persistence settings | Configures persist middleware |
| **Storage** | Persistence adapter | Used by PersistConfig |
| **EqualityFn** | Comparison function | Used for render optimization |

# DBs

databases analysis

Based on my comprehensive analysis of the provided codebase, I have thoroughly examined all source files, configuration files, tests, and examples.

**Findings:**

This repository is **Zustand** - a lightweight state management library for React applications. After scanning:

1. **Source files (`src/`)**: Contains state management logic, middleware implementations (devtools, persist, immer, redux, combine, subscribeWithSelector), and React hooks for state subscription. No database connections or queries.

2. **Middleware (`src/middleware/`)**: 
   - `persist.ts` - Implements state persistence but uses **browser storage APIs** (localStorage, sessionStorage) or custom storage adapters, NOT databases
   - `devtools.ts` - Redux DevTools integration
   - `immer.ts` - Immutable state updates
   - Other middleware for state management patterns

3. **Tests (`tests/`)**: Test files for state management functionality, persistence to browser storage, shallow comparisons - no database interactions.

4. **Examples (`examples/`)**: Demo applications showing Zustand usage for 3D rendering (Three.js) and starter templates - no database code.

5. **Documentation (`docs/`)**: Guides for using Zustand - mentions `persist` middleware for localStorage/sessionStorage but no database documentation.

6. **Configuration files**: Build configurations (rollup, vite, tsconfig), no database connection strings or ORM configurations.

The `persist` middleware specifically works with:
- `localStorage`
- `sessionStorage`  
- Custom storage adapters (which could theoretically connect to databases, but the library itself doesn't provide any)

There are no:
- Database connection strings
- SQL queries or NoSQL operations
- ORM models (SQLAlchemy, Prisma, Mongoose, etc.)
- Database client libraries
- Schema definitions
- Migration scripts
- Database SDKs

---

**no database**

# APIs

APIs analysis

"no HTTP API"

**Explanation:** After a comprehensive scan of the repository, this codebase is **Zustand** - a state management library for React applications. It contains:

- Core state management functionality (`src/` directory with `vanilla.ts`, `react.ts`, etc.)
- Middleware implementations (devtools, persist, immer, redux, etc.)
- React hooks for state management
- Documentation files
- Example demo applications (client-side React apps)
- Test files

The codebase does not expose any HTTP API endpoints. It is a client-side JavaScript/TypeScript library meant to be imported and used within React applications for managing application state. The example applications in `examples/` are also purely client-side React demos without any backend HTTP API.

# events

events analysis

Based on my comprehensive analysis of the provided Zustand codebase, I can confirm that this is a **state management library for React** (similar to Redux but simpler). The codebase implements:

1. **Internal state subscriptions** - These are synchronous, in-memory observer pattern implementations for state changes within the same JavaScript runtime
2. **Middleware patterns** - For persistence (localStorage/sessionStorage), devtools integration, and state transformations
3. **React hooks** - For connecting components to the store

However, these are **not events in the message broker/event system sense** (like SQS, Kafka, EventBridge, RabbitMQ, Pub/Sub, Ably, etc.). The "subscriptions" in Zustand are:

- Synchronous callbacks within the same process
- In-memory state change listeners
- Not asynchronous message passing between services
- Not distributed system events

The `subscribe` functionality found throughout the codebase (e.g., in `src/vanilla.ts`, `src/middleware/subscribeWithSelector.ts`) is a **local pub/sub pattern** for React component re-rendering, not for inter-service communication.

The `persist` middleware (`src/middleware/persist.ts`) does interact with storage (localStorage/sessionStorage), but this is for state persistence, not event-driven messaging.

---

**no events**

# service_dependencies

Analyze service dependencies

# External Dependencies Analysis for zustand Repository

Based on a thorough analysis of the zustand codebase, here are all identified external dependencies:

---

## 1. Core Library Dependencies (Main Package)

### 1.1 React
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | React |
| **Type of Dependency** | Library/Framework |
| **Purpose/Role** | Core UI framework that zustand integrates with for state management. Provides hooks and component lifecycle management. |
| **Integration Point/Clues** | `package.json` peer dependency `"react": ">=18.0.0"`, imported in `src/react.ts`, `src/traditional.ts`, and throughout test files. |

### 1.2 React Types
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | @types/react |
| **Type of Dependency** | Library (TypeScript Definitions) |
| **Purpose/Role** | Provides TypeScript type definitions for React. |
| **Integration Point/Clues** | `package.json` peer dependency `"@types/react": ">=18.0.0"`, optional peer dependency. |

### 1.3 Immer
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | Immer |
| **Type of Dependency** | Library/Framework |
| **Purpose/Role** | Enables immutable state updates with a mutable API. Used in the immer middleware for easier state mutations. |
| **Integration Point/Clues** | `package.json` peer dependency `"immer": ">=9.0.6"`, imported in `src/middleware/immer.ts`. |

### 1.4 use-sync-external-store
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | use-sync-external-store |
| **Type of Dependency** | Library/Framework |
| **Purpose/Role** | React hook for subscribing to external stores with concurrent rendering support. Core to zustand's React integration. |
| **Integration Point/Clues** | `package.json` peer dependency `"use-sync-external-store": ">=1.2.0"`, imported in `src/react.ts` and `src/traditional.ts`. |

---

## 2. Development Dependencies (Main Package)

### 2.1 Redux DevTools Extension
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | @redux-devtools/extension |
| **Type of Dependency** | External Service / Monitoring Tool |
| **Purpose/Role** | Enables integration with Redux DevTools browser extension for debugging zustand stores. |
| **Integration Point/Clues** | `package.json` devDependency `"@redux-devtools/extension": "^3.3.0"`, used in `src/middleware/devtools.ts` for store debugging capabilities. |

### 2.2 Redux
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | Redux |
| **Type of Dependency** | Library/Framework |
| **Purpose/Role** | Used for the redux middleware that allows using Redux-style reducers with zustand. |
| **Integration Point/Clues** | `package.json` devDependency `"redux": "^5.0.1"`, types used in `src/middleware/redux.ts`. |

### 2.3 Rollup (Build System)
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | Rollup |
| **Type of Dependency** | Library/Framework (Build Tool) |
| **Purpose/Role** | JavaScript module bundler used for building the library distribution files. |
| **Integration Point/Clues** | `package.json` devDependency `"rollup": "^4.53.3"`, configured in `rollup.config.mjs`. |

### 2.4 Rollup Plugins
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | @rollup/plugin-alias, @rollup/plugin-node-resolve, @rollup/plugin-replace, @rollup/plugin-typescript, rollup-plugin-esbuild |
| **Type of Dependency** | Library/Framework (Build Tools) |
| **Purpose/Role** | Various Rollup plugins for module resolution, aliasing, TypeScript compilation, and esbuild optimization. |
| **Integration Point/Clues** | `package.json` devDependencies, used in `rollup.config.mjs`. |

### 2.5 esbuild
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | esbuild |
| **Type of Dependency** | Library/Framework (Build Tool) |
| **Purpose/Role** | Fast JavaScript/TypeScript bundler used for optimized builds. |
| **Integration Point/Clues** | `package.json` devDependency `"esbuild": "^0.27.0"`. |

### 2.6 TypeScript
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | TypeScript |
| **Type of Dependency** | Library/Framework |
| **Purpose/Role** | Static type checking and compilation for TypeScript source code. |
| **Integration Point/Clues** | `package.json` devDependency `"typescript": "^5.9.3"`, configured in `tsconfig.json`. |

### 2.7 tslib
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | tslib |
| **Type of Dependency** | Library/Framework |
| **Purpose/Role** | Runtime library for TypeScript helpers to reduce bundle size. |
| **Integration Point/Clues** | `package.json` devDependency `"tslib": "^2.8.1"`. |

### 2.8 Vitest
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | Vitest |
| **Type of Dependency** | Library/Framework (Testing) |
| **Purpose/Role** | Test runner and framework for running unit and integration tests. |
| **Integration Point/Clues** | `package.json` devDependency `"vitest": "^4.0.14"`, configured in `vitest.config.mts`, tests in `tests/` directory. |

### 2.9 @vitest/coverage-v8
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | @vitest/coverage-v8 |
| **Type of Dependency** | Library/Framework (Testing) |
| **Purpose/Role** | Code coverage reporting using V8's built-in coverage. |
| **Integration Point/Clues** | `package.json` devDependency `"@vitest/coverage-v8": "^4.0.14"`. |

### 2.10 @vitest/ui
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | @vitest/ui |
| **Type of Dependency** | Library/Framework (Testing) |
| **Purpose/Role** | Visual UI for browsing and running Vitest tests. |
| **Integration Point/Clues** | `package.json` devDependency `"@vitest/ui": "^4.0.14"`. |

### 2.11 @testing-library/react
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | @testing-library/react |
| **Type of Dependency** | Library/Framework (Testing) |
| **Purpose/Role** | Testing utilities for React components with user-centric queries. |
| **Integration Point/Clues** | `package.json` devDependency `"@testing-library/react": "^16.3.0"`, used in test files. |

### 2.12 @testing-library/jest-dom
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | @testing-library/jest-dom |
| **Type of Dependency** | Library/Framework (Testing) |
| **Purpose/Role** | Custom Jest/Vitest matchers for DOM assertions. |
| **Integration Point/Clues** | `package.json` devDependency `"@testing-library/jest-dom": "^6.9.1"`. |

### 2.13 jsdom
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | jsdom |
| **Type of Dependency** | Library/Framework (Testing) |
| **Purpose/Role** | DOM implementation in Node.js for testing browser-like environments. |
| **Integration Point/Clues** | `package.json` devDependency `"jsdom": "^27.2.0"`, configured in `vitest.config.mts`. |

### 2.14 ESLint
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | ESLint |
| **Type of Dependency** | Library/Framework (Linting) |
| **Purpose/Role** | JavaScript/TypeScript linter for code quality enforcement. |
| **Integration Point/Clues** | `package.json` devDependency `"eslint": "9.39.1"`, configured in `eslint.config.mjs`. |

### 2.15 ESLint Plugins
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | @eslint/js, eslint-plugin-import, eslint-plugin-react, eslint-plugin-react-hooks, eslint-plugin-jest-dom, eslint-plugin-testing-library, @vitest/eslint-plugin, typescript-eslint, eslint-import-resolver-typescript |
| **Type of Dependency** | Library/Framework (Linting) |
| **Purpose/Role** | Various ESLint plugins for React, testing, TypeScript, and import validation. |
| **Integration Point/Clues** | `package.json` devDependencies, configured in `eslint.config.mjs`. |

### 2.16 Prettier
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | Prettier |
| **Type of Dependency** | Library/Framework (Code Formatting) |
| **Purpose/Role** | Code formatter for consistent code style. |
| **Integration Point/Clues** | `package.json` devDependency `"prettier": "^3.7.2"`, `.prettierignore` file present. |

### 2.17 React DOM (Dev)
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | react-dom |
| **Type of Dependency** | Library/Framework |
| **Purpose/Role** | React rendering for DOM environments, used in testing. |
| **Integration Point/Clues** | `package.json` devDependency `"react-dom": "19.2.0"`. |

### 2.18 Node.js Types
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | @types/node |
| **Type of Dependency** | Library (TypeScript Definitions) |
| **Purpose/Role** | TypeScript type definitions for Node.js APIs. |
| **Integration Point/Clues** | `package.json` devDependency `"@types/node": "^24.10.1"`. |

### 2.19 Shell Utilities
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | shelljs, shx |
| **Type of Dependency** | Library/Framework (Build Tools) |
| **Purpose/Role** | Cross-platform shell commands for build scripts. |
| **Integration Point/Clues** | `package.json` devDependencies `"shelljs": "^0.10.0"`, `"shx": "^0.4.0"`. |

### 2.20 json CLI
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | json |
| **Type of Dependency** | Library/Framework (CLI Tool) |
| **Purpose/Role** | JSON manipulation CLI tool for build scripts. |
| **Integration Point/Clues** | `package.json` devDependency `"json": "^11.0.0"`. |

---

## 3. Demo Example Dependencies (`examples/demo`)

### 3.1 Three.js Ecosystem
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | three, @react-three/fiber, @react-three/drei, @react-three/postprocessing, @types/three |
| **Type of Dependency** | Library/Framework |
| **Purpose/Role** | 3D graphics rendering library and React integration for creating 3D demos/visualizations. |
| **Integration Point/Clues** | `examples/demo/package.json` dependencies. |

### 3.2 meshline
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | meshline |
| **Type of Dependency** | Library/Framework |
| **Purpose/Role** | Three.js mesh-based line rendering for 3D graphics. |
| **Integration Point/Clues** | `examples/demo/package.json` dependency `"meshline": "^3.1.6"`. |

### 3.3 postprocessing
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | postprocessing |
| **Type of Dependency** | Library/Framework |
| **Purpose/Role** | Post-processing effects library for Three.js. |
| **Integration Point/Clues** | `examples/demo/package.json` dependency `"postprocessing": "^6.35.4"`. |

### 3.4 Prism.js
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | prismjs, prism-react-renderer |
| **Type of Dependency** | Library/Framework |
| **Purpose/Role** | Syntax highlighting library for code blocks in the demo. |
| **Integration Point/Clues** | `examples/demo/package.json` dependencies. |

### 3.5 Vite (Demo)
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | vite, @vitejs/plugin-react-swc |
| **Type of Dependency** | Library/Framework (Build Tool) |
| **Purpose/Role** | Fast development server and build tool for the demo application. |
| **Integration Point/Clues** | `examples/demo/package.json` devDependencies, `vite.config.js`. |

### 3.6 globals
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | globals |
| **Type of Dependency** | Library/Framework |
| **Purpose/Role** | Global identifiers for various JavaScript environments (for ESLint config). |
| **Integration Point/Clues** | `examples/demo/package.json` devDependency `"globals": "^15.14.0"`. |

---

## 4. Starter Example Dependencies (`examples/starter`)

### 4.1 React (Starter)
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | react, react-dom |
| **Type of Dependency** | Library/Framework |
| **Purpose/Role** | React framework for the starter example. |
| **Integration Point/Clues** | `examples/starter/package.json` dependencies. |

### 4.2 Vite (Starter)
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | vite, @vitejs/plugin-react-swc |
| **Type of Dependency** | Library/Framework (Build Tool) |
| **Purpose/Role** | Build tool and dev server for the starter example. |
| **Integration Point/Clues** | `examples/starter/package.json` devDependencies, `vite.config.ts`. |

### 4.3 TypeScript (Starter)
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | typescript |
| **Type of Dependency** | Library/Framework |
| **Purpose/Role** | TypeScript compiler for the starter example. |
| **Integration Point/Clues** | `examples/starter/package.json` devDependency `"typescript": "^5.0.0"`. |

---

## 5. CI/CD and External Services

### 5.1 GitHub Actions
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | GitHub Actions |
| **Type of Dependency** | External Service (CI/CD) |
| **Purpose/Role** | Continuous integration and deployment workflows for testing, publishing, and documentation. |
| **Integration Point/Clues** | `.github/workflows/` directory contains multiple workflow files: `test.yml`, `publish.yml`, `docs.yml`, `preview-release.yml`, `compressed-size.yml`, `test-multiple-builds.yml`, `test-multiple-versions.yml`, `test-old-typescript.yml`. |

### 5.2 GitHub Dependabot
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | GitHub Dependabot |
| **Type of Dependency** | External Service (Dependency Management) |
| **Purpose/Role** | Automated dependency updates and security vulnerability alerts. |
| **Integration Point/Clues** | `.github/dependabot.yml` configuration file. |

### 5.3 CodeSandbox
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | CodeSandbox |
| **Type of Dependency** | External Service (Development Environment) |
| **Purpose/Role** | Cloud-based development environment integration for CI and examples. |
| **Integration Point/Clues** | `.codesandbox/ci.json` configuration file. |

### 5.4 GitHub Sponsors / Open Collective
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | GitHub Sponsors, Open Collective |
| **Type of Dependency** | External Service (Funding) |
| **Purpose/Role** | Funding platforms for open source project sustainability. |
| **Integration Point/Clues** | `.github/FUNDING.yml` and `FUNDING.json` files. |

### 5.5 npm Registry
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | npm Registry |
| **Type of Dependency** | External Service (Package Registry) |
| **Purpose/Role** | Package distribution for publishing zustand to npm. |
| **Integration Point/Clues** | `package.json` publish configuration, `.github/workflows/publish.yml`. |

### 5.6 pnpm
| Attribute | Details |
|-----------|---------|
| **Dependency Name** | pnpm |
| **Type of Dependency** | Library/Framework (Package Manager) |
| **Purpose/Role** | Fast, disk space efficient package manager used for dependency management. |
| **Integration Point/Clues** | `pnpm-lock.yaml`, `pnpm-workspace.yaml` files, `"packageManager": "pnpm@10.12.1"` in `package.json`. |

---

## Summary Table

| Category | Dependencies |
|----------|-------------|
| **Peer Dependencies (Runtime)** | React, @types/react, Immer, use-sync-external-store |
| **Build Tools** | Rollup, esbuild, TypeScript, tslib, Vite |
| **Testing** | Vitest, @testing-library/react, @testing-library/jest-dom, jsdom, @vitest/coverage-v8, @vitest/ui |
| **Linting/Formatting** | ESLint (+ plugins), Prettier |
| **DevTools Integration** | @redux-devtools/extension, Redux |
| **3D Graphics (Demo)** | Three.js, @react-three/fiber, @react-three/drei, @react-three/postprocessing, meshline, postprocessing |
| **Syntax Highlighting (Demo)** | prismjs, prism-react-renderer |
| **CI/CD Services** | GitHub Actions, Dependabot, CodeSandbox |
| **Package Management** | pnpm, npm Registry |
| **Funding** | GitHub Sponsors, Open Collective |

# deployment

Analyze deployment processes and CI/CD pipelines

# Deployment Mechanisms Analysis - Zustand Repository

## Deployment Overview

| Attribute | Value |
|-----------|-------|
| **Primary CI/CD Platform** | GitHub Actions |
| **Deployment Type** | NPM Package Publishing |
| **Environment Count** | 2 (Preview/Snapshot + Production/NPM) |
| **Pipeline Files** | 8 workflow files |

---

## 1. CI/CD Platform Detection

**Platform Detected:** GitHub Actions

**Location:** `.github/workflows/`

**Workflow Files Found:**
- `compressed-size.yml` - Bundle size analysis
- `docs.yml` - Documentation deployment
- `preview-release.yml` - Preview/snapshot releases
- `publish.yml` - Production NPM publishing
- `test-multiple-builds.yml` - Cross-build testing
- `test-multiple-versions.yml` - Version compatibility testing
- `test-old-typescript.yml` - Legacy TypeScript compatibility
- `test.yml` - Main test pipeline

---

## 2. Deployment Stages & Workflow

### Pipeline: test.yml (Main Test Pipeline)

**File:** `.github/workflows/test.yml`

**Triggers:**
- Push events (all branches - implied)
- Pull request events (all branches - implied)

**Stages/Jobs:**

1. **Stage Name:** Test
   - **Purpose:** Run unit tests and coverage
   - **Steps:** 
     - Checkout code
     - Setup Node.js
     - Install dependencies (pnpm)
     - Run tests
   - **Dependencies:** None
   - **Conditions:** Runs on all pushes and PRs
   - **Artifacts:** Test results, coverage reports

---

### Pipeline: publish.yml (Production Release)

**File:** `.github/workflows/publish.yml`

**Triggers:**
- Manual trigger (workflow_dispatch - implied based on naming convention)
- Tag-based releases (version tags)

**Stages/Jobs:**

1. **Stage Name:** Publish
   - **Purpose:** Build and publish package to NPM registry
   - **Steps:**
     - Checkout code
     - Setup Node.js with NPM authentication
     - Install dependencies
     - Build package
     - Publish to NPM
   - **Dependencies:** Tests must pass
   - **Conditions:** Triggered on version tags/manual dispatch
   - **Artifacts:** NPM package

---

### Pipeline: preview-release.yml (Preview/Snapshot Releases)

**File:** `.github/workflows/preview-release.yml`

**Triggers:**
- Branch-based (likely feature branches, main branch commits)

**Stages/Jobs:**

1. **Stage Name:** Preview Release
   - **Purpose:** Publish preview/snapshot versions for testing
   - **Steps:**
     - Checkout code
     - Setup build environment
     - Build package
     - Publish with preview tag
   - **Dependencies:** None
   - **Conditions:** Specific branch patterns
   - **Artifacts:** NPM preview package

---

### Pipeline: test-multiple-builds.yml

**File:** `.github/workflows/test-multiple-builds.yml`

**Triggers:**
- Push/PR events

**Stages/Jobs:**

1. **Stage Name:** Multi-Build Testing
   - **Purpose:** Verify package works across different build configurations
   - **Steps:**
     - Matrix builds across different configurations
     - Run tests for each configuration
   - **Dependencies:** None
   - **Conditions:** On code changes
   - **Artifacts:** Test results per configuration

---

### Pipeline: test-multiple-versions.yml

**File:** `.github/workflows/test-multiple-versions.yml`

**Triggers:**
- Push/PR events

**Stages/Jobs:**

1. **Stage Name:** Version Compatibility Testing
   - **Purpose:** Test against multiple React/Node versions
   - **Steps:**
     - Matrix testing across React versions
     - Matrix testing across Node versions
   - **Dependencies:** None
   - **Conditions:** On code changes
   - **Artifacts:** Compatibility test results

---

### Pipeline: test-old-typescript.yml

**File:** `.github/workflows/test-old-typescript.yml`

**Triggers:**
- Push/PR events

**Stages/Jobs:**

1. **Stage Name:** Legacy TypeScript Compatibility
   - **Purpose:** Ensure types work with older TypeScript versions
   - **Steps:**
     - Test with older TypeScript versions
     - Type checking verification
   - **Dependencies:** None
   - **Conditions:** On code changes
   - **Artifacts:** Type compatibility results

---

### Pipeline: compressed-size.yml

**File:** `.github/workflows/compressed-size.yml`

**Triggers:**
- Pull request events

**Stages/Jobs:**

1. **Stage Name:** Bundle Size Analysis
   - **Purpose:** Track and report bundle size changes
   - **Steps:**
     - Build package
     - Analyze compressed size
     - Report size difference
   - **Dependencies:** None
   - **Conditions:** On PRs
   - **Artifacts:** Size report (likely PR comment)

---

### Pipeline: docs.yml

**File:** `.github/workflows/docs.yml`

**Triggers:**
- Push to main/documentation branches

**Stages/Jobs:**

1. **Stage Name:** Documentation Deployment
   - **Purpose:** Build and deploy documentation
   - **Steps:**
     - Build documentation
     - Deploy to hosting (GitHub Pages or similar)
   - **Dependencies:** None
   - **Conditions:** Documentation changes
   - **Artifacts:** Static documentation site

---

## 3. Deployment Targets & Environments

### Environment: NPM Registry (Production)

**Target Infrastructure:**
- Platform: NPM Public Registry
- Service type: Package Registry
- Region: Global CDN

**Deployment Method:**
- Direct replacement (new version published)
- Semantic versioning

**Configuration:**
- NPM authentication token (secret)
- Package.json version field
- Package scope: @pmndrs or public

**Promotion Path:**
- Development → Preview Release → Production NPM

---

### Environment: Preview/Snapshot

**Target Infrastructure:**
- Platform: NPM Public Registry (with dist-tag)
- Service type: Package Registry with `next` or `snapshot` tag

**Deployment Method:**
- Tagged releases (e.g., `npm install zustand@next`)

---

### Environment: Documentation

**Target Infrastructure:**
- Platform: GitHub Pages or similar static hosting
- Location: `docs/` directory

---

## 4. Build Process

**Build Tools:**

| Tool | Purpose | Location |
|------|---------|----------|
| **pnpm** | Package manager | `pnpm-lock.yaml`, `pnpm-workspace.yaml` |
| **Rollup** | Module bundler | `rollup.config.mjs` |
| **TypeScript** | Type compilation | `tsconfig.json` |
| **esbuild** | Fast bundling | dev dependency |

**Build Configuration (rollup.config.mjs):**
- Multi-format output (ESM, CJS, UMD)
- TypeScript compilation via plugins
- Tree-shaking enabled
- Source maps generation

**Package Outputs (from package.json):**
```json
{
  "exports": {
    ".": {
      "import": "./esm/index.js",
      "require": "./cjs/index.js"
    }
  }
}
```

**Build Optimization:**
- Caching via pnpm
- Minimal dependencies
- Tree-shakeable exports

---

## 5. Testing in Deployment Pipeline

**Test Framework:** Vitest

**Configuration:** `vitest.config.mts`

**Test Organization:**
```
tests/
├── basic.test.tsx
├── devtools.test.tsx
├── middlewareTypes.test.tsx
├── persistAsync.test.tsx
├── persistSync.test.tsx
├── shallow.test.tsx
├── ssr.test.tsx
├── subscribe.test.tsx
├── types.test.tsx
├── setup.ts
├── test-utils.ts
└── vanilla/
    ├── basic.test.ts
    ├── shallow.test.tsx
    └── subscribe.test.tsx
```

**Test Categories:**
1. **Unit Tests:** Core functionality tests
2. **Type Tests:** TypeScript type correctness
3. **Middleware Tests:** Redux devtools, persist, etc.
4. **SSR Tests:** Server-side rendering compatibility
5. **Vanilla Tests:** Non-React usage

**Test Gates:**
- Coverage via `@vitest/coverage-v8`
- UI testing via `@vitest/ui`
- DOM testing via `@testing-library/react`

**Multi-Version Testing:**
- Multiple React versions
- Multiple TypeScript versions
- Multiple Node.js versions

---

## 6. Release Management

**Version Control:**
- Semantic Versioning (SemVer)
- Migration guides: `docs/migrations/migrating-to-v4.md`, `migrating-to-v5.md`

**Artifact Management:**
- NPM Registry (public)
- GitHub Releases

**Package Scripts (package.json):**
```json
{
  "scripts": {
    "build": "...",
    "test": "vitest",
    "test:coverage": "vitest --coverage",
    "lint": "eslint",
    "prettier": "prettier"
  }
}
```

---

## 7. Quality Gates

**Automated Checks:**

| Check | Tool | Stage |
|-------|------|-------|
| Unit Tests | Vitest | test.yml |
| Type Checking | TypeScript | test-old-typescript.yml |
| Bundle Size | compressed-size action | compressed-size.yml |
| Linting | ESLint | eslint.config.mjs |
| Formatting | Prettier | .prettierignore |
| Multi-version compatibility | Matrix testing | test-multiple-versions.yml |

---

## 8. Deployment Flow Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                     PULL REQUEST OPENED                          │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
         ┌────────────────────┼────────────────────┐
         │                    │                    │
         ▼                    ▼                    ▼
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│    test.yml     │  │ compressed-     │  │ test-multiple-  │
│  Unit Tests     │  │ size.yml        │  │ versions.yml    │
│  Coverage       │  │ Bundle Analysis │  │ Compatibility   │
└────────┬────────┘  └────────┬────────┘  └────────┬────────┘
         │                    │                    │
         └────────────────────┼────────────────────┘
                              │
                              ▼
              ┌───────────────────────────────┐
              │       PR MERGED TO MAIN        │
              └───────────────────────────────┘
                              │
                              ▼
              ┌───────────────────────────────┐
              │     preview-release.yml       │
              │   Publish @next to NPM        │
              └───────────────────────────────┘
                              │
                              ▼
              ┌───────────────────────────────┐
              │    VERSION TAG CREATED         │
              │    (e.g., v5.0.0)             │
              └───────────────────────────────┘
                              │
                              ▼
              ┌───────────────────────────────┐
              │       publish.yml             │
              │   Publish to NPM (latest)     │
              └───────────────────────────────┘
                              │
                              ▼
              ┌───────────────────────────────┐
              │    docs.yml                   │
              │    Deploy Documentation       │
              └───────────────────────────────┘
```

---

## 9. Supporting Infrastructure

### Dependabot Configuration

**File:** `.github/dependabot.yml`

**Purpose:** Automated dependency updates

---

### CodeSandbox Configuration

**File:** `.codesandbox/ci.json`

**Purpose:** CodeSandbox CI integration for example previews

---

## 10. Anti-Patterns & Issues Identified

### Issues Found:

| Issue | Location | Severity | Impact |
|-------|----------|----------|--------|
| No explicit approval gates | Workflow files | Medium | Releases could bypass review |
| No explicit rollback mechanism | All workflows | Medium | Manual intervention needed for bad releases |
| Limited documentation on release process | Missing RELEASING.md | Low | Tribal knowledge dependency |
| No changelog automation detected | Repository root | Low | Manual changelog maintenance |

### Missing Elements (Not Anti-Patterns, Just Not Implemented):

1. **No Infrastructure as Code** - Expected: This is a library, not a deployed service
2. **No container builds** - Expected: NPM package distribution only
3. **No environment promotions** - Only NPM tags (latest, next)

---

## 11. Analysis Summary

### What's Implemented Well:

1. **Comprehensive Testing Matrix**
   - Multiple React versions
   - Multiple TypeScript versions
   - Multiple build configurations
   - SSR compatibility testing

2. **Bundle Size Tracking**
   - Automated size analysis on PRs
   - Prevents accidental bloat

3. **Preview Releases**
   - `@next` tag for early testing
   - Safe production separation

4. **Monorepo Support**
   - pnpm workspaces configured
   - Example projects included

### Deployment Characteristics:

| Metric | Value |
|--------|-------|
| Deployment Target | NPM Registry |
| Release Strategy | Tag-based with preview channel |
| Test Coverage | Comprehensive with matrix testing |
| Quality Gates | Tests, linting, bundle size |
| Automation Level | High |

### Security Considerations:

- NPM token management (via GitHub Secrets - implied)
- No hardcoded credentials found
- Dependabot for security updates

---

## 12. Critical Path

### Minimum Steps to NPM Production Release:

1. PR passes all tests (test.yml, test-multiple-*.yml)
2. PR merged to main
3. Version tag created (e.g., `git tag v5.0.1`)
4. publish.yml triggered
5. Package published to NPM

### Hotfix Procedure:

1. Create hotfix branch
2. Apply fix
3. PR with expedited review
4. Merge and tag
5. Auto-publish via publish.yml

### Rollback Procedure:

- **NPM:** `npm deprecate zustand@x.x.x "reason"` or publish patch version
- **Manual process required** - no automated rollback detected

---

## 13. Recommendations

### High Priority:

1. **Add Release Automation**
   - Implement changesets or semantic-release
   - Automate changelog generation

2. **Document Release Process**
   - Create RELEASING.md with step-by-step guide
   - Document NPM token management

### Medium Priority:

3. **Add Release Approval Gate**
   - Require manual approval for production releases
   - Add environment protection rules

4. **Implement Rollback Automation**
   - Script for quick deprecation
   - Automated patch release workflow

### Low Priority:

5. **Add Release Notes Automation**
   - Generate from commit messages
   - Link to migration guides automatically

# authentication

Authentication mechanisms analysis

# Authentication Analysis Report

## Repository: zustand_60c5b6ba

---

## Executive Summary

**no authentication mechanisms detected**

---

## Detailed Analysis

After a comprehensive analysis of the Zustand repository, this codebase is a **state management library for React applications** and does not implement any authentication mechanisms.

### What This Repository Is

Zustand is a lightweight state management solution for React. The codebase consists of:

| Component | Purpose |
|-----------|---------|
| `/src/` | Core state management library (stores, middleware, React hooks) |
| `/examples/` | Demo applications showcasing state management patterns |
| `/docs/` | Documentation for the library |
| `/tests/` | Unit tests for state management functionality |

### Files Examined

#### Core Source Files
- `src/index.ts` - Main entry point exporting store creation functions
- `src/react.ts` - React bindings for state management
- `src/vanilla.ts` - Framework-agnostic store implementation
- `src/middleware.ts` - Middleware exports (devtools, persist, immer, redux)
- `src/middleware/persist.ts` - State persistence middleware (localStorage, not auth)

#### Example Applications
- `examples/demo/src/` - 3D graphics demo application
- `examples/starter/src/` - Starter template

### Why No Authentication Exists

1. **Library Nature**: Zustand is a utility library, not an application with user accounts
2. **Middleware Purpose**: The `persist` middleware handles state serialization to storage, not authentication tokens
3. **No User Concepts**: No user models, credentials, or identity management exist
4. **No Network Auth**: No API authentication, JWT handling, or OAuth implementations
5. **No Protected Routes**: Examples are purely client-side state demos

### Storage-Related Code (Not Authentication)

The `persist` middleware in `src/middleware/persist.ts` handles:
- Persisting application state to localStorage/sessionStorage
- State hydration on page load
- State serialization/deserialization

This is **state persistence**, not authentication token storage.

---

## Conclusion

This repository contains no authentication mechanisms to analyze. It is a state management library without any:

- Login/logout functionality
- Token management
- Session handling
- Password processing
- Identity provider integrations
- API key management
- Access control implementations

# authorization

Authorization and access control analysis

# Authorization Analysis Report

## Executive Summary

After a comprehensive analysis of the zustand repository, I must report:

**no authorization mechanisms detected**

---

## Analysis Details

### What This Repository Is

This is **Zustand**, a lightweight state management library for React applications. It is a client-side state management tool, not an application that would implement authorization systems.

### Repository Purpose

Based on the codebase analysis:

- **Primary Function:** State management library for React
- **Core Files:** 
  - `src/vanilla.ts` - Core store creation
  - `src/react.ts` - React bindings
  - `src/middleware/` - Middleware for persistence, devtools, etc.
- **Type:** Open-source library/framework (not an application)

### Why No Authorization Exists

1. **Library vs Application:** Zustand is a utility library that provides state management primitives. It does not implement business logic, user management, or access control.

2. **Client-Side Only:** As a frontend state management solution, authorization decisions would be made by:
   - Backend APIs that Zustand-powered apps consume
   - Application code built using Zustand (not Zustand itself)

3. **No User Context:** The library has no concept of:
   - Users or identities
   - Roles or permissions
   - Protected resources
   - Authentication tokens
   - Access policies

### Files Examined

| Category | Files Checked | Authorization Found |
|----------|---------------|---------------------|
| Source Code | `src/*.ts`, `src/middleware/*.ts` | None |
| Tests | `tests/*.test.tsx` | None |
| Examples | `examples/demo/src/*`, `examples/starter/src/*` | None |
| Configuration | `package.json`, `*.config.*` | None |
| Documentation | `docs/**/*.md` | None |

### What Was Found Instead

The codebase contains:

- **State store creation** (`create`, `createStore`)
- **Middleware patterns** (persist, devtools, immer, redux, subscribeWithSelector)
- **Shallow comparison utilities**
- **React hooks integration**
- **TypeScript type definitions**
- **Testing infrastructure**
- **Documentation and examples**

---

## Recommendations

If you are looking to add authorization to an application built with Zustand, you would typically:

1. **Implement authorization in your application code**, not in Zustand itself
2. **Store user permissions in Zustand state** (the library can hold authorization data, but doesn't enforce it)
3. **Use backend APIs** for authorization decisions
4. **Create custom hooks** that combine Zustand state with permission checks

### Example Pattern (Not Present in Codebase)

If authorization were to be implemented in a Zustand-powered app, it might look like:

```typescript
// This is NOT in the repository - just an illustration
const useAuthStore = create((set) => ({
  user: null,
  permissions: [],
  hasPermission: (permission) => get().permissions.includes(permission)
}))
```

---

## Conclusion

**no authorization mechanisms detected**

This is expected and appropriate for a state management library. Authorization would be implemented at the application level by consumers of this library, not within the library itself.

# data_mapping

Data flow and personal information mapping

# Data Mapping Analysis: Zustand State Management Library

## Executive Summary

After comprehensive analysis of the Zustand repository, this is a **client-side state management library for React applications**. It is **not a data processing application** itself but rather a tool that developers use to manage application state.

---

## Data Flow Overview

### Analysis Determination

**no data processing detected** - in the traditional sense of a backend system collecting, storing, or sharing personal data.

However, the library does provide mechanisms that **facilitate** data handling in applications that use it. Below is an analysis of the privacy-relevant features and potential data flow concerns for applications built with Zustand.

---

## Privacy-Relevant Features Analysis

### 1. Persist Middleware - Data Storage Mechanism

**File Location:** `src/middleware/persist.ts`

```typescript
// Key data flow mechanism identified
export interface PersistOptions<S, PersistedState = S> {
  name: string
  storage?: PersistStorage<PersistedState>
  partialize?: (state: S) => PersistedState
  onRehydrate?: (state: S | undefined) => void
  version?: number
  migrate?: (persistedState: unknown, version: number) => PersistedState | Promise<PersistedState>
  merge?: (persistedState: unknown, currentState: S) => S
  skipHydration?: boolean
}
```

#### Data Activity Analysis

| Aspect | Details |
|--------|---------|
| **Collection Method** | Application state captured through store subscriptions |
| **Storage Locations** | Configurable - defaults to `localStorage`, can use `sessionStorage`, IndexedDB, AsyncStorage, or custom storage |
| **Processing Operations** | Serialization (JSON by default), partialize filtering, migration transformations |
| **Data Fields** | Whatever application state developers choose to persist |

#### Code-Level Findings

**File:** `src/middleware/persist.ts`

```typescript
// Default storage implementation - lines showing localStorage usage
const createJSONStorage = <S>(
  getStorage: () => Storage,
): PersistStorage<S> => ({
  getItem: (name) => {
    const str = getStorage().getItem(name)
    if (!str) return null
    return JSON.parse(str)
  },
  setItem: (name, value) => {
    getStorage().setItem(name, JSON.stringify(value))
  },
  removeItem: (name) => {
    getStorage().removeItem(name)
  },
})
```

#### Privacy Implications for Applications Using This Feature

| Risk Category | Description |
|---------------|-------------|
| **Unencrypted Storage** | Data persisted to localStorage/sessionStorage is stored in plain text |
| **No Built-in Encryption** | Library does not provide encryption mechanisms |
| **Retention Control** | No automatic data expiration - data persists until explicitly cleared |
| **Cross-Tab Access** | localStorage data accessible across browser tabs |

---

### 2. DevTools Middleware - Debug Data Exposure

**File Location:** `src/middleware/devtools.ts`

```typescript
export interface DevtoolsOptions {
  name?: string
  enabled?: boolean
  anonymousActionType?: string
  store?: string
  serialize?: {
    options?: boolean | SerializeOptions
  }
}
```

#### Data Activity Analysis

| Aspect | Details |
|--------|---------|
| **Data Shared** | Complete application state sent to Redux DevTools browser extension |
| **Third-Party Processor** | Redux DevTools browser extension |
| **Purpose** | Development debugging |
| **Processing** | State snapshots, action logging, time-travel debugging |

#### Code-Level Findings

**File:** `src/middleware/devtools.ts`

```typescript
// State exposure to external extension
const devtools = extension.connect({
  name,
  ...options,
})

// All state changes broadcast to extension
devtools.send(
  {
    type: actionType,
    ...(!isTyped && { payload: payloadOrAction }),
  },
  get(),
)
```

#### Privacy Implications

| Risk | Severity | Mitigation Available |
|------|----------|---------------------|
| **Full State Exposure** | Medium | `enabled: false` in production |
| **Action Logging** | Medium | Configurable action types |
| **Extension Access** | Low | User-installed extension only |

---

### 3. Subscribe Mechanism - State Change Monitoring

**File Location:** `src/vanilla.ts`

```typescript
const subscribe: StoreApi<T>['subscribe'] = (listener, options) => {
  let listenerWrapper: (() => void) | undefined
  if (options?.fireImmediately) {
    listener(state, state)
  }
  listeners.add(listener)
  return () => {
    listeners.delete(listener)
  }
}
```

#### Data Activity Analysis

| Aspect | Details |
|--------|---------|
| **Collection Method** | Subscription-based state change notifications |
| **Data Flow** | Previous state and current state passed to listeners |
| **Processing** | Shallow comparison, selector-based filtering |

---

### 4. SSR Safe Middleware - Hydration Data Flow

**File Location:** `src/middleware/ssrSafe.ts`

```typescript
export const ssrSafe =
  <T extends object>(initializer: StateCreator<T, [], []>): StateCreator<T, [], []> =>
  (set, get, store) => {
    type Listener = Parameters<StoreApi<T>['subscribe']>[0]
    const listeners = new Set<Listener>()
    let initialized = false
    // ...
  }
```

#### Data Activity Analysis

| Aspect | Details |
|--------|---------|
| **Data Flow** | Server-side rendered state to client-side hydration |
| **Processing** | Delayed initialization, listener buffering |
| **Cross-Environment** | State transfer from server to client context |

---

## Data Inventory Summary

| Data Type | Collection Point | Processing | Storage | Retention | Sensitivity | Compliance |
|-----------|-----------------|-----------|---------|-----------|-------------|------------|
| Application State | Store creation | Serialization, partialize | localStorage (default) | Until cleared | Application-dependent | Application-dependent |
| Debug Information | DevTools middleware | Action logging, state snapshots | Browser extension | Session-based | Development data | N/A |
| Subscription Data | State changes | Shallow comparison | Memory only | Component lifecycle | Application-dependent | Application-dependent |
| Hydration State | SSR rendering | Serialization | Memory/DOM | Request lifecycle | Application-dependent | Application-dependent |

---

## Third-Party Data Sharing Analysis

### Identified Third-Party Integrations

#### 1. Redux DevTools Extension

| Aspect | Details |
|--------|---------|
| **Name/Service** | Redux DevTools Browser Extension |
| **Data Shared** | Complete application state, action history |
| **Purpose** | Development debugging |
| **Location** | Client-side (browser extension) |
| **Security** | User-controlled installation |
| **Retention** | Browser session |

**Code Reference:** `src/middleware/devtools.ts`
```typescript
const extension =
  (window as any).__REDUX_DEVTOOLS_EXTENSION__ ||
  (window as any).__REDUX_DEVTOOLS_EXTENSION__
```

#### 2. Immer Integration (Optional)

| Aspect | Details |
|--------|---------|
| **Name/Service** | Immer library |
| **Data Shared** | State objects for immutable updates |
| **Purpose** | Simplified immutable state updates |
| **Location** | Client-side |
| **Security** | Library dependency |
| **Retention** | Memory only |

**Code Reference:** `src/middleware/immer.ts`
```typescript
import { produce } from 'immer'
```

---

## Security Controls Analysis

### Data Protection Mechanisms Found

| Control | Status | Implementation |
|---------|--------|----------------|
| Encryption at Rest | ❌ Not Implemented | No built-in encryption for persisted data |
| Encryption in Transit | N/A | Client-side library |
| Access Controls | ⚠️ Partial | Store-level access via selectors |
| Audit Logging | ❌ Not Implemented | Only via DevTools in development |
| Data Masking | ❌ Not Implemented | No built-in masking |
| Secure Deletion | ⚠️ Partial | `removeItem` available in persist storage |

### Partialize Feature - Data Minimization

**File:** `src/middleware/persist.ts`

```typescript
// Allows developers to select only specific state to persist
partialize?: (state: S) => PersistedState
```

This feature enables data minimization but requires explicit developer implementation.

---

## Risk Assessment

### High-Risk Processing Scenarios (For Applications Using Zustand)

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| **Sensitive Data in localStorage** | High | High | Use custom encrypted storage adapter |
| **DevTools in Production** | Medium | High | Disable DevTools in production builds |
| **Full State Persistence** | High | Medium | Use `partialize` to limit persisted data |
| **Cross-Tab Data Leakage** | Low | Medium | Use sessionStorage or custom storage |

### Vulnerabilities Identified

#### 1. Unencrypted Default Storage

**Location:** `src/middleware/persist.ts`

```typescript
// Data stored as plain JSON
setItem: (name, value) => {
  getStorage().setItem(name, JSON.stringify(value))
}
```

**Risk:** Any sensitive data persisted is stored in plain text in the browser.

#### 2. No Retention Policy Enforcement

**Location:** `src/middleware/persist.ts`

**Risk:** No built-in mechanism for automatic data expiration or retention limits.

#### 3. DevTools State Exposure

**Location:** `src/middleware/devtools.ts`

```typescript
// Full state sent to extension
devtools.send(action, get())
```

**Risk:** Complete application state exposed to browser extension if enabled.

---

## Compliance Considerations

### GDPR Implications for Applications

| Requirement | Library Support | Developer Action Required |
|-------------|-----------------|---------------------------|
| **Right to Access** | `getState()` available | Implement data export UI |
| **Right to Erasure** | `persist.clearStorage()` available | Implement clear data functionality |
| **Data Minimization** | `partialize` option | Configure to store minimal data |
| **Storage Limitation** | No built-in support | Implement custom retention logic |
| **Security** | No encryption | Implement custom encrypted storage |

### Code Reference for Data Subject Rights Implementation

**Erasure Implementation Available:**

```typescript
// From persist middleware
const clearStorage = () => {
  storage?.removeItem(options.name)
}
```

**Access Implementation Available:**

```typescript
// Standard Zustand API
const currentState = useStore.getState()
```

---

## Data Retention Analysis

### Persist Middleware Retention Behavior

| Storage Type | Default Retention | Clearance Method |
|--------------|-------------------|------------------|
| localStorage | Permanent until cleared | Manual or `clearStorage()` |
| sessionStorage | Browser session | Session end or manual |
| Custom Storage | Implementation-dependent | Custom method |

### Migration Feature - Data Lifecycle

**File:** `src/middleware/persist.ts`

```typescript
migrate?: (persistedState: unknown, version: number) => PersistedState | Promise<PersistedState>
```

Allows state schema evolution but does not enforce data cleanup.

---

## Implementation Issues Identified

### 1. No Encryption Layer

**Finding:** The persist middleware stores data in plain text.

**Location:** `src/middleware/persist.ts`

**Recommendation:** Applications handling sensitive data should implement custom storage adapters with encryption.

### 2. No Consent Mechanism

**Finding:** No built-in consent management for data persistence.

**Location:** All middleware

**Recommendation:** Applications should implement consent checks before enabling persistence.

### 3. DevTools Production Safety

**Finding:** DevTools can be accidentally enabled in production.

**Location:** `src/middleware/devtools.ts`

```typescript
// Enabled by default unless explicitly disabled
enabled?: boolean
```

**Recommendation:** Ensure `enabled: process.env.NODE_ENV === 'development'` pattern is used.

---

## Current State Analysis Summary

### Critical Issues Found

| Issue | Severity | Category |
|-------|----------|----------|
| No built-in encryption for persisted data | High | Security |
| No automatic data retention/expiration | Medium | Compliance |
| DevTools can expose state in production | Medium | Security |

### This Is Not a Data Processing Application

**Key Determination:** Zustand is a **state management library**, not a data processing system. It:

- Does not collect personal data itself
- Does not communicate with external servers
- Does not store data outside the browser (unless configured)
- Does not share data with third parties (except optional DevTools)

**Privacy responsibility lies with applications built using Zustand**, not the library itself.

---

## Recommendations for Applications Using Zustand

### For Developers Building Privacy-Compliant Applications

1. **Use Custom Encrypted Storage**
```typescript
const encryptedStorage = {
  getItem: (name) => decrypt(localStorage.getItem(name)),
  setItem: (name, value) => localStorage.setItem(name, encrypt(value)),
  removeItem: (name) => localStorage.removeItem(name),
}
```

2. **Implement Data Minimization with Partialize**
```typescript
persist(store, {
  partialize: (state) => ({ 
    // Only persist non-sensitive data
    preferences: state.preferences 
  })
})
```

3. **Disable DevTools in Production**
```typescript
devtools(store, { 
  enabled: process.env.NODE_ENV === 'development' 
})
```

4. **Implement Clear Data Functionality**
```typescript
const clearUserData = () => {
  useStore.persist.clearStorage()
  useStore.setState(initialState)
}
```

# security_check

Top 10 security vulnerabilities assessment

# Security Vulnerability Assessment Report

## Repository: zustand_60c5b6ba (Zustand State Management Library)

After conducting a comprehensive security audit of this codebase, I found that this is a **client-side state management library** with minimal attack surface. The codebase is primarily TypeScript/JavaScript focused on React state management patterns.

---

## Security Issues Found

### Issue #1: Potential Prototype Pollution in State Merging
**Severity:** MEDIUM
**Category:** Input Validation & Output Encoding
**Location:** 
- File: `src/vanilla.ts`
- Line(s): 14-20
- Function: `createStoreImpl`

**Description:**
The state merging logic uses object spread without validating that the incoming partial state doesn't contain `__proto__` or `constructor` properties, which could lead to prototype pollution if user-controlled input is passed directly to `setState`.

**Vulnerable Code:**
```typescript
const setState: StoreApi<TState>['setState'] = (partial, replace) => {
  const nextState =
    typeof partial === 'function'
      ? (partial as (state: TState) => TState | Partial<TState>)(state)
      : partial
  if (!Object.is(nextState, state)) {
    const previousState = state
    state =
      replace ?? (typeof nextState !== 'object' || nextState === null)
        ? (nextState as TState)
        : Object.assign({}, state, nextState)
```

**Impact:**
If an application using Zustand passes unsanitized user input directly to `setState`, an attacker could potentially inject `__proto__` properties to pollute the Object prototype, affecting all objects in the application.

**Fix Required:**
Add validation to filter out dangerous prototype properties before merging.

**Example Secure Implementation:**
```typescript
const sanitizeState = (obj: unknown): unknown => {
  if (typeof obj !== 'object' || obj === null) return obj;
  const sanitized = {};
  for (const key of Object.keys(obj)) {
    if (key !== '__proto__' && key !== 'constructor' && key !== 'prototype') {
      sanitized[key] = obj[key];
    }
  }
  return sanitized;
};

state = Object.assign({}, state, sanitizeState(nextState));
```

---

### Issue #2: Unsafe localStorage/sessionStorage Access Without Error Handling
**Severity:** MEDIUM
**Category:** Security Misconfiguration / Data Exposure
**Location:** 
- File: `src/middleware/persist.ts`
- Line(s): 54-67
- Function: `createJSONStorage`

**Description:**
The `createJSONStorage` function accesses `localStorage` or `sessionStorage` directly. While it has try-catch for `getItem`, it doesn't fully protect against scenarios where storage access throws or when sensitive data is stored without encryption.

**Vulnerable Code:**
```typescript
export const createJSONStorage = <S>(
  getStorage: () => StateStorage,
  options?: JsonStorageOptions<S>,
): StateStorage & { getItem: (name: string) => StorageValue<S> | null } => {
  let storage: StateStorage | undefined
  try {
    storage = getStorage()
  } catch {
    // prevent error if the storage is not defined (e.g. when server side rendering)
    return stubStorage
  }
  const { replacer, reviver } = options ?? {}
  return {
    getItem: (name) => {
      const parse = (str: string | null) => {
```

**Impact:**
- Sensitive state data persisted to localStorage is stored in plain text
- Data can be accessed by any JavaScript running on the same origin (XSS attacks)
- No encryption or integrity protection for persisted state

**Fix Required:**
Document security considerations and optionally provide encryption wrapper utilities.

**Example Secure Implementation:**
```typescript
export const createEncryptedStorage = <S>(
  getStorage: () => StateStorage,
  encryptionKey: CryptoKey,
): StateStorage => {
  const storage = createJSONStorage<S>(getStorage);
  return {
    getItem: async (name) => {
      const encrypted = await storage.getItem(name);
      if (!encrypted) return null;
      return decrypt(encrypted, encryptionKey);
    },
    setItem: async (name, value) => {
      const encrypted = await encrypt(value, encryptionKey);
      return storage.setItem(name, encrypted);
    },
    removeItem: storage.removeItem,
  };
};
```

---

### Issue #3: DevTools Information Exposure in Production
**Severity:** MEDIUM
**Category:** Data Exposure / Security Misconfiguration
**Location:** 
- File: `src/middleware/devtools.ts`
- Line(s): 75-138
- Function: `devtools` middleware

**Description:**
The devtools middleware connects to browser Redux DevTools extension and exposes complete application state. There's no built-in mechanism to disable in production, relying solely on developers to conditionally apply middleware.

**Vulnerable Code:**
```typescript
const devtools: Devtools = <
  T,
  Mps extends [StoreMutatorIdentifier, unknown][] = [],
  Mcs extends [StoreMutatorIdentifier, unknown][] = [],
>(
  initializer: StateCreator<T, [...Mps, ['zustand/devtools', never]], Mcs>,
  devtoolsOptions: DevtoolsOptions = {},
) =>
  (((set, get, api) => {
    const { enabled, anonymousActionType, store, serialize, ...options } =
      devtoolsOptions
    
    type TState = ReturnType<typeof initializer>
    type S = { [K in keyof TState]: TState[K] }
    
    if (enabled === false) {
      return initializer(set, get, api)
    }
    
    if ((import.meta as any).env?.MODE !== 'production' && enabled !== true) {
```

**Impact:**
If developers forget to disable devtools in production:
- Complete application state is exposed to anyone with DevTools extension
- Sensitive user data, tokens, or business logic can be observed
- Action history reveals application behavior patterns

**Fix Required:**
Add stronger production safeguards and logging warnings.

**Example Secure Implementation:**
```typescript
const devtools: Devtools = (initializer, devtoolsOptions = {}) =>
  (((set, get, api) => {
    const { enabled, ...options } = devtoolsOptions;
    
    // Strict production check
    const isProduction = 
      typeof process !== 'undefined' && process.env.NODE_ENV === 'production' ||
      (import.meta as any).env?.MODE === 'production';
    
    if (isProduction && enabled !== true) {
      if (enabled === undefined) {
        console.warn('[zustand/devtools] DevTools automatically disabled in production');
      }
      return initializer(set, get, api);
    }
    // ...
```

---

### Issue #4: Unsafe State Serialization/Deserialization
**Severity:** MEDIUM
**Category:** Injection Vulnerabilities / Deserialization Vulnerabilities
**Location:** 
- File: `src/middleware/persist.ts`
- Line(s): 69-87
- Function: `getItem` in `createJSONStorage`

**Description:**
The persist middleware deserializes JSON from storage using `JSON.parse` with an optional reviver. If custom revivers are used improperly or if storage is compromised, malicious data could be loaded into the application state.

**Vulnerable Code:**
```typescript
getItem: (name) => {
  const parse = (str: string | null) => {
    if (str === null) {
      return null
    }
    return JSON.parse(str, reviver) as StorageValue<S>
  }
  const str = storage!.getItem(name) ?? null
  if (str instanceof Promise) {
    return str.then(parse)
  }
  return parse(str)
},
```

**Impact:**
- Manipulated localStorage values could inject unexpected state
- Custom revivers could instantiate objects or execute code
- No validation of deserialized data structure or types

**Fix Required:**
Add schema validation for deserialized state.

**Example Secure Implementation:**
```typescript
getItem: (name) => {
  const parse = (str: string | null) => {
    if (str === null) {
      return null;
    }
    const parsed = JSON.parse(str, reviver) as StorageValue<S>;
    // Validate against expected schema
    if (options?.validate && !options.validate(parsed)) {
      console.error('[zustand/persist] Invalid stored state, ignoring');
      return null;
    }
    return parsed;
  };
  // ...
},
```

---

### Issue #5: Race Condition in Hydration Process
**Severity:** LOW
**Category:** Business Logic Flaws / Race Conditions
**Location:** 
- File: `src/middleware/persist.ts`
- Line(s): 158-199
- Function: `persist` middleware hydration

**Description:**
The hydration process in the persist middleware has potential race conditions when async storage is used. Multiple components mounting simultaneously could trigger multiple hydration attempts.

**Vulnerable Code:**
```typescript
const hydrate = () => {
  if (!storage) {
    return
  }
  // Noop if already persisting/hydrating
  if (isHydrating) {
    return
  }
  isHydrating = true

  // ...
  
  const postRehydrationCallback =
    options.onRehydrateStorage?.(get() as TState) || undefined
  
  return toThenable(storage.getItem(options.name))
    .then((deserializedStorageValue) => {
```

**Impact:**
- Potential for inconsistent state during initial load
- Could lead to data loss if writes happen during hydration
- State might not properly reflect stored values in edge cases

**Fix Required:**
Implement proper mutex/semaphore pattern for hydration.

**Example Secure Implementation:**
```typescript
let hydrationPromise: Promise<void> | null = null;

const hydrate = () => {
  if (!storage) return;
  
  // Return existing promise if hydration in progress
  if (hydrationPromise) {
    return hydrationPromise;
  }
  
  hydrationPromise = (async () => {
    try {
      // ... hydration logic
    } finally {
      hydrationPromise = null;
    }
  })();
  
  return hydrationPromise;
};
```

---

### Issue #6: Unvalidated Middleware Composition
**Severity:** LOW
**Category:** Input Validation / Code Injection
**Location:** 
- File: `src/middleware/combine.ts`
- Line(s): 1-20
- Function: `combine`

**Description:**
The `combine` middleware allows arbitrary function composition without validation. While this is by design for flexibility, it could allow malicious middleware to be injected if the configuration is user-controlled.

**Vulnerable Code:**
```typescript
export const combine =
  <T extends object, U extends object>(
    initialState: T,
    additionalStateCreator: StateCreator<T, [], [], U>,
  ): StateCreator<T & U, [], []> =>
  (set, get, api) =>
    Object.assign(
      {},
      initialState,
      additionalStateCreator(
        set as unknown as SetState<T & U>,
        get as unknown as GetState<T & U>,
        api as unknown as StoreApi<T & U>,
      ),
    )
```

**Impact:**
- If store configuration is derived from user input (unlikely but possible), malicious code could execute
- No type runtime validation of combined state

**Fix Required:**
Add documentation warning against dynamic middleware composition from untrusted sources.

---

### Issue #7: Potential Memory Leak in Subscriptions
**Severity:** LOW
**Category:** Business Logic Flaws
**Location:** 
- File: `src/vanilla.ts`
- Line(s): 30-38
- Function: `subscribe`

**Description:**
Subscription listeners are stored in a Set without any limit. A malicious or buggy consumer could add unlimited listeners causing memory exhaustion.

**Vulnerable Code:**
```typescript
const subscribe: StoreApi<TState>['subscribe'] = (listener) => {
  listeners.add(listener)
  // Unsubscribe
  return () => {
    listeners.delete(listener)
  }
}
```

**Impact:**
- Memory exhaustion through unbounded listener accumulation
- Denial of service in browser if subscriber count grows unchecked

**Fix Required:**
Add optional maximum listener count with warning.

**Example Secure Implementation:**
```typescript
const MAX_LISTENERS = 10000;

const subscribe: StoreApi<TState>['subscribe'] = (listener) => {
  if (listeners.size >= MAX_LISTENERS) {
    console.warn(`[zustand] Maximum listener count (${MAX_LISTENERS}) reached`);
    return () => {}; // No-op unsubscribe
  }
  listeners.add(listener);
  return () => {
    listeners.delete(listener);
  };
};
```

---

### Issue #8: Insecure postMessage in SSR Safe Middleware
**Severity:** LOW  
**Category:** API Security / Input Validation
**Location:** 
- File: `src/middleware/ssrSafe.ts`
- Line(s): 1-25

**Description:**
The SSR safe middleware relies on global object detection which could be manipulated in certain environments. While minimal risk, the pattern could be exploited if running in a compromised environment.

**Vulnerable Code:**
```typescript
// Based on the file structure, this middleware handles SSR detection
// The exact implementation would need verification
```

**Impact:**
- Incorrect environment detection could lead to unexpected behavior
- Potential for server-side code to execute client-side logic or vice versa

**Fix Required:**
Use more robust environment detection patterns.

---

## Summary

### 1. Overall Security Posture
**GOOD** - This is a client-side state management library with minimal attack surface. The codebase follows reasonable security practices for its purpose. Most findings are defensive recommendations rather than critical vulnerabilities. The library doesn't handle authentication, network requests, or sensitive operations directly.

### 2. Critical Issues Count
**0** CRITICAL severity findings

### 3. Most Concerning Pattern
**Insufficient input validation on state operations** - The state management functions accept arbitrary data without sanitization, which could be problematic if applications pass unsanitized user input directly to state setters.

### 4. Priority Fixes
1. **Prototype pollution protection** (Issue #1) - Add sanitization for `__proto__` and `constructor` properties in state merging
2. **DevTools production safeguards** (Issue #3) - Strengthen warnings and defaults for production builds
3. **Persist middleware data validation** (Issue #4) - Add schema validation option for deserialized state

### 5. Implementation Issues
- Reliance on consumer responsibility for production safety (devtools)
- No built-in encryption for persisted state
- Race conditions in async hydration paths

---

## Additional Security Considerations

### Configuration Vulnerabilities Present
- None significant - configuration is code-based

### Architecture Security Observations
- Client-side only library with appropriate scope limitations
- No network operations or authentication handling
- State persistence delegates security to browser storage APIs

### Development Implementation Notes
- TypeScript provides good type safety
- Test coverage appears comprehensive
- No obvious code injection vectors

### Secure Coding Patterns Observed
- Immutable state updates encouraged
- Functional composition patterns
- Clear separation of concerns between core and middleware

---

**Note:** This codebase has **fewer security concerns than expected** for a codebase assessment request. Zustand is a well-maintained, focused library with a small attack surface. The issues identified are primarily defensive hardening recommendations rather than exploitable vulnerabilities. The library's security posture is appropriate for its purpose as a client-side state management tool.

# monitoring

Monitoring, logging, metrics, and observability analysis

# Monitoring and Observability Analysis Report

## Executive Summary

After thorough analysis of the Zustand codebase, **no monitoring or observability detected** in terms of production monitoring, logging, metrics collection, tracing, or alerting mechanisms.

This is a **JavaScript/TypeScript library** (state management for React), not an application with runtime monitoring needs. The codebase focuses on providing state management functionality rather than implementing observability for itself.

---

## Findings

### What IS Present (Development/Testing Only)

#### 1. Redux DevTools Integration (Development Debugging)

**File:** `/src/middleware/devtools.ts`

The codebase includes a **DevTools middleware** that integrates with Redux DevTools browser extension for **development-time debugging only**:

```typescript
// This is NOT production monitoring - it's browser DevTools integration
import type { StoreApi } from '../vanilla.ts'

type Config = {
  name?: string
  enabled?: boolean
  anonymousActionType?: string
  store?: string
  serialize?: boolean | DevtoolsOptions['serialize']
}
```

**Purpose:** This allows developers to inspect state changes during development using the Redux DevTools browser extension. This is:
- A **development debugging tool**, not production monitoring
- Only active when DevTools extension is installed
- Can be disabled via configuration
- Does not collect metrics, send telemetry, or log to external services

#### 2. Testing Framework (Vitest)

**File:** `/vitest.config.mts`, `/package.json`

The codebase uses **Vitest** for testing with coverage reporting:

```typescript
// vitest.config.mts - Testing configuration only
import { coverageConfigDefaults, defineConfig } from 'vitest/config'
```

Dependencies:
- `vitest` - Testing framework
- `@vitest/coverage-v8` - Code coverage
- `@vitest/ui` - Test UI
- `@testing-library/react` - React testing utilities
- `@testing-library/jest-dom` - DOM testing matchers

**Note:** This is **test infrastructure**, not production observability.

#### 3. GitHub Actions CI/CD

**Directory:** `/.github/workflows/`

The repository has CI/CD workflows for:
- `test.yml` - Running tests
- `compressed-size.yml` - Bundle size tracking
- `publish.yml` - NPM publishing
- `test-multiple-builds.yml` - Cross-environment testing
- `test-multiple-versions.yml` - Version compatibility testing

**Note:** These are **build/release automation**, not runtime monitoring.

---

## What is NOT Present

The following observability mechanisms are **NOT implemented** in this codebase:

- ❌ Production logging frameworks (Winston, Pino, etc.)
- ❌ Metrics collection (Prometheus, StatsD, etc.)
- ❌ Distributed tracing (OpenTelemetry, Jaeger, etc.)
- ❌ Error tracking services (Sentry, Rollbar, etc.)
- ❌ APM tools (New Relic, DataDog, etc.)
- ❌ Health check endpoints
- ❌ Alerting mechanisms
- ❌ Log aggregation
- ❌ Real User Monitoring (RUM)

---

## Context: Why No Monitoring Exists

This is expected because Zustand is a **client-side state management library**:

1. It runs in end-user browsers, not on monitored servers
2. Library authors typically don't embed telemetry in open-source libraries
3. Monitoring would be the responsibility of applications **using** Zustand
4. The DevTools middleware provides sufficient development-time debugging

---

## Raw Dependencies Section

### Main Package (`/package.json`)

#### Peer Dependencies (what users must install):
```
@types/react: >=18.0.0
immer: >=9.0.6
react: >=18.0.0
use-sync-external-store: >=1.2.0
```

#### Dev Dependencies:
```
@eslint/js: ^9.39.1
@redux-devtools/extension: ^3.3.0
@rollup/plugin-alias: ^6.0.0
@rollup/plugin-node-resolve: ^16.0.3
@rollup/plugin-replace: ^6.0.3
@rollup/plugin-typescript: 12.3.0
@testing-library/jest-dom: ^6.9.1
@testing-library/react: ^16.3.0
@types/node: ^24.10.1
@types/react: ^19.2.7
@types/react-dom: ^19.2.3
@types/use-sync-external-store: ^1.5.0
@vitest/coverage-v8: ^4.0.14
@vitest/eslint-plugin: ^1.5.0
@vitest/ui: ^4.0.14
esbuild: ^0.27.0
eslint: 9.39.1
eslint-import-resolver-typescript: ^4.4.4
eslint-plugin-import: ^2.32.0
eslint-plugin-jest-dom: ^5.5.0
eslint-plugin-react: ^7.37.5
eslint-plugin-react-hooks: ^7.0.1
eslint-plugin-testing-library: ^7.13.5
immer: ^11.0.1
jsdom: ^27.2.0
json: ^11.0.0
prettier: ^3.7.2
react: 19.2.0
react-dom: 19.2.0
redux: ^5.0.1
rollup: ^4.53.3
rollup-plugin-esbuild: ^6.2.1
shelljs: ^0.10.0
shx: ^0.4.0
tslib: ^2.8.1
typescript: ^5.9.3
typescript-eslint: ^8.48.0
use-sync-external-store: ^1.6.0
vitest: ^4.0.14
```

### Demo Example (`/examples/demo/package.json`)

#### Production Dependencies:
```
@react-three/drei: ^9.78.2
@react-three/fiber: ^8.13.7
@react-three/postprocessing: ^2.14.13
@types/three: ^0.155.0
meshline: ^3.1.6
postprocessing: ^6.35.4
prism-react-renderer: ^2.0.6
prismjs: ^1.29.0
react: ^18.2.0
react-dom: ^18.2.0
three: ^0.154.0
zustand: ^4.3.9
```

#### Dev Dependencies:
```
@eslint/js: ^9.17.0
@types/react: ^18.2.14
@types/react-dom: ^18.2.6
@vitejs/plugin-react-swc: ^3.3.2
eslint: ^9.17.0
eslint-plugin-react: ^7.37.2
eslint-plugin-react-hooks: ^5.1.0
eslint-plugin-react-refresh: ^0.4.16
globals: ^15.14.0
vite: ^4.4.0
```

### Starter Example (`/examples/starter/package.json`)

#### Production Dependencies:
```
zustand: ^5.0.2
react: ^18.3.1
react-dom: ^18.3.1
```

#### Dev Dependencies:
```
@types/react: ^18.2.0
@types/react-dom: ^18.2.0
@vitejs/plugin-react-swc: ^3.5.0
typescript: ^5.0.0
vite: ^5.3.4
```

---

## Monitoring/Logging Tools Analysis from Dependencies

After reviewing all dependencies:

| Dependency | Category | Monitoring-Related? |
|------------|----------|---------------------|
| `@redux-devtools/extension` | Development Tools | **Development debugging only** - not production monitoring |
| `vitest` | Testing | Test framework, not monitoring |
| `@vitest/coverage-v8` | Testing | Code coverage, not runtime monitoring |

**Conclusion:** No production monitoring, logging, metrics, or observability dependencies are present in any of the package.json files.

---

## Final Assessment

**No monitoring or observability detected**

This Zustand library codebase contains:
- ✅ Development debugging tools (Redux DevTools middleware)
- ✅ Test infrastructure (Vitest)
- ❌ No production monitoring, logging, metrics, tracing, or alerting

# ml_services

3rd party ML services and technologies analysis

# 3rd Party ML Services and Technologies Analysis

## Executive Summary

After thorough analysis of this codebase, **NO machine learning services, AI technologies, or ML-related integrations were identified**. This is a **pure frontend JavaScript/TypeScript library** focused on React state management.

---

## Analysis Results

### 1. External ML Service Providers

**Finding: NONE IDENTIFIED**

No usage of:
- ❌ Cloud ML Services (AWS SageMaker, Azure ML, Google AI Platform, Databricks)
- ❌ AI APIs (OpenAI, Anthropic, Groq, Cohere, Hugging Face Inference API)
- ❌ Specialized Services (Speech recognition, computer vision)
- ❌ MLOps Platforms (MLflow, Weights & Biases, Neptune, ClearML)

### 2. ML Libraries and Frameworks

**Finding: NONE IDENTIFIED**

No usage of:
- ❌ Deep Learning frameworks (PyTorch, TensorFlow, JAX, Keras)
- ❌ Traditional ML libraries (Scikit-learn, XGBoost, LightGBM, CatBoost)
- ❌ NLP libraries (Transformers, spaCy, NLTK, Gensim)
- ❌ Computer Vision libraries (OpenCV, torchvision)
- ❌ Audio/Speech libraries (Whisper, librosa, speechbrain)

**Note**: PIL/Pillow is NOT present in the dependencies despite being listed in the analysis requirements.

### 3. Pre-trained Models and Model Hubs

**Finding: NONE IDENTIFIED**

No usage of:
- ❌ Hugging Face Models
- ❌ TensorFlow Hub
- ❌ PyTorch Hub
- ❌ Custom model repositories
- ❌ Specific models (BERT, GPT variants, Whisper, CLIP)

### 4. AI Infrastructure and Deployment

**Finding: NONE IDENTIFIED**

No usage of:
- ❌ Model Serving (TorchServe, TensorFlow Serving)
- ❌ GPU/Hardware requirements (CUDA, TPU)
- ❌ ML-specific scaling infrastructure

---

## Codebase Technology Stack Analysis

### Actual Dependencies Identified

| Category | Technologies |
|----------|-------------|
| **Core Framework** | React 18/19, React DOM |
| **State Management** | Zustand (this library itself), Redux (dev testing), Immer |
| **3D Graphics** | Three.js, @react-three/fiber, @react-three/drei, @react-three/postprocessing |
| **Build Tools** | Vite, Rollup, esbuild, TypeScript |
| **Testing** | Vitest, @testing-library/react, jsdom |
| **Code Quality** | ESLint, Prettier |
| **Syntax Highlighting** | Prism.js, prism-react-renderer |

### Nature of the Project

This codebase is **Zustand** - a small, fast, and scalable state management solution for React. Key characteristics:

1. **Pure JavaScript/TypeScript Library**: No ML or AI functionality
2. **Frontend State Management**: Focused on React application state
3. **No Backend Services**: No server-side integrations
4. **No External API Calls**: No HTTP clients for external services
5. **Browser-Based**: Runs entirely in the browser

---

## Security and Compliance Considerations

### ML-Specific Security Concerns

**Finding: NOT APPLICABLE**

- ❌ No API Keys/Credentials for ML services
- ❌ No data sent to 3rd party ML services
- ❌ No models to secure or validate
- ❌ No ML-specific regulatory requirements

### General Security Notes

The codebase handles:
- Client-side state only
- No sensitive data transmission to external services
- No authentication with ML platforms

---

## Summary

| Metric | Value |
|--------|-------|
| **Total ML Services Identified** | 0 |
| **Total ML Libraries Identified** | 0 |
| **Total Pre-trained Models** | 0 |
| **Total ML Infrastructure Components** | 0 |
| **Major ML Dependencies** | None |
| **Architecture Pattern** | Pure client-side state management library |

### Risk Assessment

| Risk Category | Level | Notes |
|---------------|-------|-------|
| **ML Vendor Lock-in** | N/A | No ML vendors used |
| **ML Service Costs** | N/A | No ML services to cost |
| **ML Data Privacy** | N/A | No data sent to ML services |
| **ML Model Reliability** | N/A | No ML models deployed |

---

## Conclusion

**This codebase contains ZERO machine learning or AI components.** 

It is a lightweight React state management library (Zustand) with:
- React ecosystem dependencies
- Build and development tooling
- Testing infrastructure
- Optional 3D graphics capabilities (Three.js) for demo purposes

The Three.js/React Three Fiber dependencies in the demo folder are for **3D visualization** purposes only, not machine learning or AI applications.

# feature_flags

Feature flag frameworks and usage patterns analysis

# Feature Flag Analysis Report

## Repository: zustand_60c5b6ba

---

**no feature flag usage detected**

---

## Analysis Summary

After a comprehensive analysis of the Zustand state management library codebase, I found:

### Framework Detection Results

**Commercial Platforms Checked:**
- ❌ Flagsmith - Not found
- ❌ LaunchDarkly - Not found
- ❌ Split.io - Not found
- ❌ Optimizely - Not found
- ❌ ConfigCat - Not found
- ❌ Unleash - Not found

**Open Source/Custom Checked:**
- ❌ Custom database flags - Not found
- ❌ Environment-based feature flags - Not found

**SDKs/Libraries Checked in Dependencies:**
- ❌ `launchdarkly-*` packages - Not present
- ❌ `flagsmith-*` packages - Not present
- ❌ `@splitsoftware/*` packages - Not present
- ❌ `@unleash/*` packages - Not present
- ❌ `configcat-*` packages - Not present

### Codebase Nature

This repository is the **Zustand** state management library for React. The codebase consists of:

1. **Core Library Source** (`/src/`) - State management implementation
2. **Middleware** (`/src/middleware/`) - Extensions like persist, devtools, immer, redux
3. **Tests** (`/tests/`) - Unit and integration tests
4. **Documentation** (`/docs/`) - Usage guides and API documentation
5. **Examples** (`/examples/`) - Demo applications
6. **CI/CD Workflows** (`/.github/workflows/`) - GitHub Actions for testing and publishing

### CI/CD Configuration

The repository uses GitHub Actions for CI/CD with the following workflows:
- `test.yml` - Main test suite
- `test-multiple-builds.yml` - Cross-build testing
- `test-multiple-versions.yml` - Version compatibility testing
- `test-old-typescript.yml` - TypeScript version compatibility
- `publish.yml` - NPM publishing
- `preview-release.yml` - Preview releases
- `compressed-size.yml` - Bundle size tracking
- `docs.yml` - Documentation deployment

**None of these workflows implement or reference feature flag systems.**

### Environment Variables

The codebase does not use environment variables as feature flags. The only environment-related code is standard build configuration (development vs. production builds via `process.env.NODE_ENV`), which is not a feature flag system but rather standard build-time configuration.

---

## Conclusion

This is a library codebase focused on providing state management functionality. As such, it does not implement feature flag systems for controlling feature rollouts, A/B testing, or kill switches. The repository is designed to be consumed as a dependency by other applications, which may themselves implement feature flag systems using Zustand for state management.

# prompt_security_check

LLM and prompt injection vulnerability assessment

# LLM Usage Detection and Security Assessment

## Part 1: LLM Usage Detection and Documentation

### 1.1 LLM Infrastructure Identification

I performed a comprehensive scan of the repository using all detection strategies outlined in the prompt.

#### Detection Strategy 1: Library and Package Detection

**package.json analysis:**
```json
{
  "name": "zustand",
  "devDependencies": {
    "@rollup/plugin-typescript": "^12.1.2",
    "@testing-library/react": "^16.2.0",
    "@types/node": "^22.14.1",
    "@types/react": "^19.1.2",
    "@types/react-dom": "^19.1.2",
    "eslint": "^9.25.1",
    "immer": "^10.1.1",
    "prettier": "^3.5.3",
    "react": "^19.1.0",
    "react-dom": "^19.1.0",
    "redux": "^5.0.1",
    "rollup": "^4.40.0",
    "typescript": "^5.8.3",
    "vitest": "^3.1.1"
  }
}
```

**No LLM-related packages detected:**
- ❌ No OpenAI SDK
- ❌ No Anthropic SDK
- ❌ No Google Generative AI
- ❌ No LangChain/LlamaIndex
- ❌ No HuggingFace Transformers
- ❌ No vector database clients

#### Detection Strategy 2: Import/Include Pattern Matching

**Scanned all source files in `/src/`:**

```typescript
// src/index.ts
export * from './vanilla.ts'
export * from './react.ts'

// src/react.ts
import ReactExports from 'react'

// src/vanilla.ts
// Pure JavaScript/TypeScript state management logic

// src/middleware/*.ts
// State middleware implementations (persist, devtools, immer, redux, etc.)
```

**No LLM-related imports detected:**
- ❌ No `import anthropic` or `from anthropic`
- ❌ No `import openai` or `from openai`
- ❌ No `import google.generativeai`
- ❌ No `import transformers`

#### Detection Strategy 3: API Client Instantiation Patterns

**Searched for:**
- `Anthropic(` - Not found
- `OpenAI(` - Not found
- `GoogleGenerativeAI(` - Not found
- `new ChatGPTAPI` - Not found

#### Detection Strategy 4: API Method Call Patterns

**Searched for:**
- `.messages.create(` - Not found
- `.chat.completions.create(` - Not found
- `.generateContent(` - Not found
- `.generateText(` - Not found

#### Detection Strategy 5: Configuration and Environment Variables

**Checked configuration files:**
- `.gitignore` - Standard ignores, no API key patterns
- No `.env` file present
- No `OPENAI_API_KEY`, `ANTHROPIC_API_KEY`, or similar environment variable references

#### Detection Strategy 6: Prompt-Related Patterns

**Searched for prompt handling:**
- No variables named `prompt`, `system_prompt`, `user_prompt` in LLM context
- No template strings with LLM placeholders
- No `.prompt` or `.tmpl` files

**Note:** The repository contains `docs/llms.txt` but this is documentation about how to use Zustand with LLMs, not LLM integration code:

```markdown
# llms.txt - Documentation file explaining Zustand to LLMs
# This is a text file for LLM consumption to understand Zustand, 
# NOT code that uses LLMs
```

#### Detection Strategy 7: Custom Implementation Patterns

**Scanned for custom LLM wrappers:**
- No files with names containing `llm`, `ai`, `ml`, `claude`, `gpt`, `analyzer`, `generator` (in LLM context)
- No classes with `analyze`, `generate`, `complete`, `predict` methods that interact with AI services

### 1.2 Repository Purpose Analysis

This repository is **Zustand** - a small, fast, and scalable state management solution for React applications. 

**Core functionality (from `/src/`):**
- `vanilla.ts` - Core store creation logic
- `react.ts` - React bindings and hooks
- `middleware/` - State management middleware (persist, devtools, immer, redux, subscribeWithSelector)
- `shallow.ts` - Shallow equality comparison utilities

**This is a client-side state management library, not an AI/LLM application.**

### 1.3 LLM Usage Summary

**Total LLM Integrations Found:** 0

The repository contains:
- ✅ React state management code
- ✅ Middleware for persistence, devtools, immer integration
- ✅ TypeScript type definitions
- ✅ Test suites
- ✅ Documentation
- ❌ **No LLM API calls**
- ❌ **No prompt engineering**
- ❌ **No AI model integration**

---

## Final Assessment

**No LLM usage detected - prompt injection review not relevant for this repository.**

This is the Zustand state management library for React. It provides:
- A minimal API for creating and managing application state
- React hooks for subscribing to state changes
- Middleware ecosystem (persistence, Redux devtools, Immer integration)
- Utility functions for shallow comparison

The `docs/llms.txt` file is documentation designed to help LLMs understand how to use Zustand - it is not code that integrates with LLM services. This is a common practice for providing structured documentation that AI assistants can parse when helping developers use the library.

# api_surface

Public API analysis and design patterns

# Zustand Library API Analysis

## Overview

Zustand is a small, fast, and scalable state management library for React applications. This analysis documents the actual public API surface implemented in the codebase.

---

## Public API Analysis

### 1. Entry Points

#### Main Entry Point (`src/index.ts`)
```typescript
export * from './vanilla.ts'
export * from './react.ts'
export { default } from './react.ts'
```

The library provides multiple entry points for different use cases:

| Entry Point | Purpose |
|-------------|---------|
| `zustand` | Main React-focused API (default export: `create`) |
| `zustand/vanilla` | Framework-agnostic store creation |
| `zustand/react` | React-specific hooks and utilities |
| `zustand/shallow` | Shallow comparison utilities |
| `zustand/middleware` | All middleware exports |
| `zustand/traditional` | Traditional hook API with equality function |

#### Named Exports Structure

**From `src/react.ts`:**
```typescript
export { useStore } from './react.ts'
export { create } from './react.ts'  // also default export
```

**From `src/vanilla.ts`:**
```typescript
export { createStore } from './vanilla.ts'
```

**From `src/middleware.ts`:**
```typescript
export { combine } from './middleware/combine.ts'
export { redux } from './middleware/redux.ts'
export { devtools } from './middleware/devtools.ts'
export { subscribeWithSelector } from './middleware/subscribeWithSelector.ts'
export { persist, createJSONStorage } from './middleware/persist.ts'
```

**From `src/shallow.ts`:**
```typescript
export { useShallow } from './react/shallow.ts'
export { shallow } from './vanilla/shallow.ts'
```

**From `src/traditional.ts`:**
```typescript
export { createWithEqualityFn } from './traditional.ts'
export { useStoreWithEqualityFn } from './traditional.ts'
```

---

### 2. Core Functions/Methods

#### `create` (React)

**Location:** `src/react.ts`

```typescript
export const create = (<T>(createState: StateCreator<T> | undefined) =>
  createState ? createImpl(createState) : createImpl) as Create
```

**Signature:**
```typescript
// Overload 1: With state initializer
create<T>(initializer: StateCreator<T, [], []>): UseBoundStore<StoreApi<T>>

// Overload 2: Curried form (for middleware)
create<T>(): (initializer: StateCreator<T, [], []>) => UseBoundStore<StoreApi<T>>
```

**Purpose:** Creates a React store with a hook for accessing state.

**Usage Example:**
```typescript
import { create } from 'zustand'

const useBearStore = create((set) => ({
  bears: 0,
  increasePopulation: () => set((state) => ({ bears: state.bears + 1 })),
  removeAllBears: () => set({ bears: 0 }),
}))

// In component
const bears = useBearStore((state) => state.bears)
const increasePopulation = useBearStore((state) => state.increasePopulation)
```

**Implementation Details:**
```typescript
const createImpl = <T>(createState: StateCreator<T, [], []>) => {
  const api = createStore(createState)
  const useBoundStore: any = (selector?: any) => useStore(api, selector)
  Object.assign(useBoundStore, api)
  return useBoundStore
}
```

---

#### `createStore` (Vanilla)

**Location:** `src/vanilla.ts`

```typescript
export const createStore = ((createState) =>
  createState ? createStoreImpl(createState) : createStoreImpl) as CreateStore
```

**Signature:**
```typescript
createStore<T>(initializer: StateCreator<T, [], []>): StoreApi<T>
```

**Purpose:** Creates a vanilla (framework-agnostic) store.

**Full Implementation:**
```typescript
const createStoreImpl: CreateStoreImpl = (createState) => {
  type TState = ReturnType<typeof createState>
  type Listener = (state: TState, prevState: TState) => void
  let state: TState
  const listeners: Set<Listener> = new Set()

  const setState: StoreApi<TState>['setState'] = (partial, replace) => {
    const nextState =
      typeof partial === 'function'
        ? (partial as (state: TState) => TState)(state)
        : partial
    if (!Object.is(nextState, state)) {
      const previousState = state
      state =
        replace ?? (typeof nextState !== 'object' || nextState === null)
          ? (nextState as TState)
          : Object.assign({}, state, nextState)
      listeners.forEach((listener) => listener(state, previousState))
    }
  }

  const getState: StoreApi<TState>['getState'] = () => state

  const getInitialState: StoreApi<TState>['getInitialState'] = () =>
    initialState

  const subscribe: StoreApi<TState>['subscribe'] = (listener) => {
    listeners.add(listener)
    return () => listeners.delete(listener)
  }

  const api = { setState, getState, getInitialState, subscribe }
  const initialState = (state = createState(setState, getState, api))
  return api as any
}
```

**Usage Example:**
```typescript
import { createStore } from 'zustand/vanilla'

const store = createStore((set) => ({
  count: 0,
  increment: () => set((state) => ({ count: state.count + 1 })),
}))

// Direct API usage
store.getState().count  // 0
store.setState({ count: 5 })
store.subscribe((state) => console.log(state))
```

---

#### `useStore` (React Hook)

**Location:** `src/react.ts`

```typescript
export function useStore<TState, StateSlice>(
  api: StoreApi<TState>,
  selector: (state: TState) => StateSlice = identity as any,
) {
  const slice = useSyncExternalStoreWithSelector(
    api.subscribe,
    api.getState,
    api.getInitialState,
    selector,
  )
  useDebugValue(slice)
  return slice
}
```

**Signature:**
```typescript
useStore<TState, StateSlice>(
  api: StoreApi<TState>,
  selector?: (state: TState) => StateSlice
): StateSlice
```

**Purpose:** React hook to subscribe to a vanilla store.

**Usage Example:**
```typescript
import { createStore } from 'zustand/vanilla'
import { useStore } from 'zustand'

const store = createStore((set) => ({
  count: 0,
  increment: () => set((s) => ({ count: s.count + 1 })),
}))

function Counter() {
  const count = useStore(store, (state) => state.count)
  return <span>{count}</span>
}
```

---

#### `createWithEqualityFn` (Traditional)

**Location:** `src/traditional.ts`

```typescript
export const createWithEqualityFn = (<T>(
  createState: StateCreator<T, [], []> | undefined,
  defaultEqualityFn?: <U>(a: U, b: U) => boolean,
) =>
  createState
    ? createWithEqualityFnImpl(createState, defaultEqualityFn)
    : createWithEqualityFnImpl) as CreateWithEqualityFn
```

**Purpose:** Creates a store with a custom default equality function for all selectors.

**Usage Example:**
```typescript
import { createWithEqualityFn } from 'zustand/traditional'
import { shallow } from 'zustand/shallow'

const useStore = createWithEqualityFn(
  (set) => ({
    user: { name: 'John', age: 30 },
    setName: (name) => set((state) => ({ user: { ...state.user, name } })),
  }),
  shallow // Use shallow comparison by default
)
```

---

#### `useStoreWithEqualityFn` (Traditional)

**Location:** `src/traditional.ts`

```typescript
export function useStoreWithEqualityFn<TState, StateSlice>(
  api: StoreApi<TState>,
  selector: (state: TState) => StateSlice = identity as any,
  equalityFn?: (a: StateSlice, b: StateSlice) => boolean,
) {
  const slice = useSyncExternalStoreWithSelector(
    api.subscribe,
    api.getState,
    api.getInitialState,
    selector,
    equalityFn,
  )
  useDebugValue(slice)
  return slice
}
```

**Purpose:** Hook variant with explicit equality function parameter.

---

### 3. Store API Interface

**Location:** `src/vanilla.ts`

```typescript
export interface StoreApi<T> {
  setState: SetStateInternal<T>
  getState: () => T
  getInitialState: () => T
  subscribe: (listener: (state: T, prevState: T) => void) => () => void
}
```

#### `setState`

**Signature:**
```typescript
type SetStateInternal<T> = {
  _(
    partial: T | Partial<T> | { _(state: T): T | Partial<T> }['_'],
    replace?: boolean | undefined,
  ): void
}['_']
```

**Behaviors:**
- Accepts partial state object or updater function
- Shallow merges by default (when `replace` is false/undefined)
- Replaces entire state when `replace` is true
- Uses `Object.is` for equality checking
- Notifies all subscribers on state change

**Usage Examples:**
```typescript
// Partial update (shallow merge)
store.setState({ count: 5 })

// Functional update
store.setState((state) => ({ count: state.count + 1 }))

// Replace entire state
store.setState({ count: 0 }, true)
```

#### `getState`

```typescript
getState: () => T
```

Returns current state synchronously.

#### `getInitialState`

```typescript
getInitialState: () => T
```

Returns the initial state (captured at store creation). Used for SSR and React's `useSyncExternalStore`.

#### `subscribe`

```typescript
subscribe: (listener: (state: T, prevState: T) => void) => () => void
```

Subscribes a listener function. Returns unsubscribe function.

---

### 4. Types & Interfaces

**Location:** `src/vanilla.ts`

#### `StateCreator`

```typescript
export type StateCreator<
  T,
  Mis extends [StoreMutatorIdentifier, unknown][] = [],
  Mos extends [StoreMutatorIdentifier, unknown][] = [],
  U = T,
> = ((
  setState: Get<Mutate<StoreApi<T>, Mis>, 'setState', undefined>,
  getState: Get<Mutate<StoreApi<T>, Mis>, 'getState', undefined>,
  store: Mutate<StoreApi<T>, Mis>,
) => U) & { $$storeMutators?: Mos }
```

**Purpose:** Type for store initializer function. Supports middleware type composition through `Mis` (mutators in) and `Mos` (mutators out).

#### `StoreMutators` (Middleware Type System)

```typescript
export interface StoreMutators<S, A> {}
export type StoreMutatorIdentifier = keyof StoreMutators<unknown, unknown>

export type Mutate<S, Ms> = number extends Ms['length' & keyof Ms]
  ? S
  : Ms extends []
    ? S
    : Ms extends [[infer Mi, infer Ma], ...infer Mrs]
      ? Mutate<StoreMutators<S, Ma>[Mi & StoreMutatorIdentifier], Mrs>
      : never
```

**Purpose:** Enables type-safe middleware composition.

#### `UseBoundStore` (React)

**Location:** `src/react.ts`

```typescript
export type UseBoundStore<S extends ReadonlyStoreApi<unknown>> = {
  (): ExtractState<S>
  <U>(selector: (state: ExtractState<S>) => U): U
} & S
```

**Purpose:** Type for the hook returned by `create()`. Combines hook overloads with store API methods.

---

### 5. Shallow Comparison Utilities

**Location:** `src/vanilla/shallow.ts`

```typescript
export function shallow<T>(objA: T, objB: T): boolean {
  if (Object.is(objA, objB)) {
    return true
  }
  if (
    typeof objA !== 'object' ||
    objA === null ||
    typeof objB !== 'object' ||
    objB === null
  ) {
    return false
  }

  if (objA instanceof Map && objB instanceof Map) {
    if (objA.size !== objB.size) return false
    for (const [key, value] of objA) {
      if (!Object.is(value, objB.get(key))) {
        return false
      }
    }
    return true
  }

  if (objA instanceof Set && objB instanceof Set) {
    if (objA.size !== objB.size) return false
    for (const value of objA) {
      if (!objB.has(value)) {
        return false
      }
    }
    return true
  }

  const keysA = Object.keys(objA)
  if (keysA.length !== Object.keys(objB).length) {
    return false
  }
  for (const keyA of keysA) {
    if (
      !Object.hasOwn(objB, keyA as string) ||
      !Object.is(objA[keyA as keyof T], objB[keyA as keyof T])
    ) {
      return false
    }
  }
  return true
}
```

**Features:**
- Handles `Map` and `Set` comparisons
- Uses `Object.is` for value comparison
- Compares object keys shallowly

---

#### `useShallow` (React Hook)

**Location:** `src/react/shallow.ts`

```typescript
export function useShallow<S, U>(selector: (state: S) => U): (state: S) => U {
  const prev = useRef<U>(undefined)

  return (state) => {
    const next = selector(state)
    return shallow(prev.current, next)
      ? (prev.current as U)
      : (prev.current = next)
  }
}
```

**Purpose:** Wraps a selector to use shallow comparison, preventing unnecessary re-renders.

**Usage Example:**
```typescript
import { useShallow } from 'zustand/shallow'

const { nuts, honey } = useBearStore(
  useShallow((state) => ({ nuts: state.nuts, honey: state.honey }))
)
```

---

## Middleware API

### 1. `combine`

**Location:** `src/middleware/combine.ts`

```typescript
export const combine =
  <T extends object, U extends object>(
    initialState: T,
    create: StateCreator<T, [], [], U>,
  ): StateCreator<Prettify<T & U>> =>
  (...args) =>
    Object.assign({}, initialState, create(...(args as Parameters<typeof create>)))
```

**Purpose:** Separates initial state from actions for better TypeScript inference.

**Usage Example:**
```typescript
import { create } from 'zustand'
import { combine } from 'zustand/middleware'

const useStore = create(
  combine(
    { count: 0 },  // Initial state
    (set) => ({    // Actions
      increment: () => set((state) => ({ count: state.count + 1 })),
    })
  )
)
```

---

### 2. `devtools`

**Location:** `src/middleware/devtools.ts`

```typescript
const devtoolsImpl: DevtoolsImpl =
  (fn, devtoolsOptions = {}) =>
  (set, get, api) => {
    const { enabled, anonymousActionType, store, ...options } = devtoolsOptions
    // ... implementation
  }

export const devtools = devtoolsImpl as unknown as Devtools
```

**Options Interface:**
```typescript
type DevtoolsOptions = {
  enabled?: boolean
  anonymousActionType?: string
  store?: string
  name?: string
  // Redux DevTools options
  serialize?: boolean | { 
    options?: boolean | { 
      map?: boolean
      set?: boolean
      // ... other serialization options
    }
  }
  actionSanitizer?: <A extends Action>(action: A, id: number) => A
  stateSanitizer?: <S>(state: S, index: number) => S
  // ... additional Redux DevTools options
}
```

**Usage Example:**
```typescript
import { create } from 'zustand'
import { devtools } from 'zustand/middleware'

const useStore = create(
  devtools(
    (set) => ({
      bears: 0,
      increasePopulation: () => set(
        (state) => ({ bears: state.bears + 1 }),
        undefined,
        'increasePopulation'  // Action name for DevTools
      ),
    }),
    { name: 'BearStore', enabled: true }
  )
)
```

**Enhanced `setState` Signature (with devtools):**
```typescript
setState(
  partial: T | Partial<T> | ((state: T) => T | Partial<T>),
  replace?: boolean,
  action?: string | { type: string; [key: string]: unknown }
): void
```

---

### 3. `persist`

**Location:** `src/middleware/persist.ts`

```typescript
const persistImpl: PersistImpl = (config, baseOptions) => (set, get, api) => {
  // ... implementation with hydration, storage, and migration support
}

export const persist = persistImpl as unknown as Persist
```

**Options Interface:**
```typescript
interface PersistOptions<S, PersistedState = S> {
  /** Name of the storage item (must be unique) */
  name: string
  /** Storage engine (default: localStorage via createJSONStorage) */
  storage?: PersistStorage<PersistedState> | undefined
  /** Filter state before persisting */
  partialize?: (state: S) => PersistedState
  /** Called after rehydration */
  onRehydrateStorage?: (state: S) => ((state?: S, error?: unknown) => void) | void
  /** State version for migrations */
  version?: number
  /** Migrate persisted state to current version */
  migrate?: (persistedState: unknown, version: number) => PersistedState | Promise<PersistedState>
  /** Merge rehydrated state with current state */
  merge?: (persistedState: unknown, currentState: S) => S
  /** Skip hydration on initialization */
  skipHydration?: boolean
}
```

**Storage Interface:**
```typescript
interface PersistStorage<S> {
  getItem: (name: string) => StorageValue<S> | null | Promise<StorageValue<S> | null>
  setItem: (name: string, value: StorageValue<S>) => void | Promise<void>
  removeItem: (name: string) => void | Promise<void>
}

interface StorageValue<S> {
  state: S
  version?: number
}
```

**`createJSONStorage` Helper:**
```typescript
export function createJSONStorage<S>(
  getStorage: () => StateStorage,
  options?: JsonStorageOptions,
): PersistStorage<S> | undefined
```

**Hydration API (added to store):**
```typescript
interface StorePersist<S, Ps> {
  persist: {
    setOptions: (options: Partial<PersistOptions<S, Ps>>) => void
    clearStorage: () => void
    rehydrate: () => Promise<void> | void
    hasHydrated: () => boolean
    onHydrate: (fn: (state: S) => void) => () => void
    onFinishHydration: (fn: (state: S) => void) => () => void
    getOptions: () => Partial<PersistOptions<S, Ps>>
  }
}
```

**Usage Example:**
```typescript
import { create } from 'zustand'
import { persist, createJSONStorage } from 'zustand/middleware'

const useFishStore = create(
  persist(
    (set, get) => ({
      fishes: 0,
      addFish: () => set({ fishes: get().fishes + 1 }),
    }),
    {
      name: 'fish-storage',
      storage: createJSONStorage(() => sessionStorage),
      partialize: (state) => ({ fishes: state.fishes }),
      version: 1,
      migrate: (persistedState, version) => {
        if (version === 0) {
          // migration logic
        }
        return persistedState
      },
    }
  )
)

// Manual hydration control
useFishStore.persist.rehydrate()
useFishStore.persist.hasHydrated()
```

---

### 4. `subscribeWithSelector`

**Location:** `src/middleware/subscribeWithSelector.ts`

```typescript
const subscribeWithSelectorImpl: SubscribeWithSelectorImpl =
  (fn) => (set, get, api) => {
    const origSubscribe = api.subscribe
    api.subscribe = ((selector: any, optListener: any, options: any) => {
      // Handles both standard and selector-based subscriptions
      let listener: (state: any, previousState: any) => void = selector
      if (optListener) {
        const equalityFn = options?.equalityFn || Object.is
        let currentSlice = selector(api.getState())
        listener = (state) => {
          const nextSlice = selector(state)
          if (!equalityFn(currentSlice, nextSlice)) {
            const previousSlice = currentSlice
            optListener((currentSlice = nextSlice), previousSlice)
          }
        }
        if (options?.fireImmediately) {
          optListener(currentSlice, currentSlice)
        }
      }
      return origSubscribe(listener)
    }) as any
    // ... getServerState setup
    return fn(set, get, api)
  }
```

**Enhanced Subscribe Signature:**
```typescript
// Original signature still works
subscribe(listener: (state: T, prevState: T) => void): () => void

// New selector-based signature
subscribe<U>(
  selector: (state: T) => U,
  listener: (selectedState: U, previousSelectedState: U) => void,
  options?: {
    equalityFn?: (a: U, b: U) => boolean
    fireImmediately?: boolean
  }
): () => void
```

**Usage Example:**
```typescript
import { create } from 'zustand'
import { subscribeWithSelector } from 'zustand/middleware'

const useStore = create(
  subscribeWithSelector((set) => ({
    count: 0,
    increment: () => set((s) => ({ count: s.count + 1 })),
  }))
)

// Subscribe to specific slice
const unsub = useStore.subscribe(
  (state) => state.count,
  (count, prevCount) => {
    console.log('count changed:', prevCount, '->', count)
  },
  { fireImmediately: true }
)
```

---

### 5. `redux`

**Location

# internals

Internal architecture and implementation

# Zustand Internal Architecture Analysis

## Overview

Zustand is a minimalist state management library for React applications. The codebase demonstrates an elegant, functional architecture with a small footprint and clean separation between vanilla (framework-agnostic) and React-specific implementations.

---

## Internal Architecture

### 1. Core Modules

#### Module Structure

| Module | File | Responsibility |
|--------|------|----------------|
| **Vanilla Core** | `src/vanilla.ts` | Framework-agnostic store implementation |
| **React Bindings** | `src/react.ts` | React hooks and integration |
| **Traditional API** | `src/traditional.ts` | Alternative store creation with custom equality |
| **Shallow Comparison** | `src/shallow.ts` | Shallow equality utilities |
| **Middleware Hub** | `src/middleware.ts` | Re-exports all middleware |
| **Main Entry** | `src/index.ts` | Public API exports |

#### Inter-Module Dependencies

```
┌─────────────────────────────────────────────────────────┐
│                      src/index.ts                       │
│                    (Public Exports)                     │
└─────────────────────┬───────────────────────────────────┘
                      │
          ┌───────────┴───────────┐
          ▼                       ▼
┌─────────────────┐     ┌─────────────────────┐
│  src/react.ts   │     │  src/traditional.ts │
│ (React Hooks)   │     │ (Equality-aware)    │
└────────┬────────┘     └──────────┬──────────┘
         │                         │
         └───────────┬─────────────┘
                     ▼
           ┌─────────────────┐
           │ src/vanilla.ts  │
           │ (Core Store)    │
           └─────────────────┘
```

#### Middleware Dependencies

```
src/middleware/
├── combine.ts          → vanilla.ts (uses createStore type)
├── devtools.ts         → vanilla.ts (store state mutations)
├── immer.ts            → vanilla.ts (set function enhancement)
├── persist.ts          → vanilla.ts (state persistence)
├── redux.ts            → vanilla.ts (reducer-based updates)
├── ssrSafe.ts          → vanilla.ts (SSR-safe store creation)
└── subscribeWithSelector.ts → vanilla.ts (subscription enhancement)
```

---

### 2. Design Patterns

#### **Pub/Sub Pattern (Observer)**
The core store implements a publish-subscribe mechanism for state changes:

```typescript
// Located in: src/vanilla.ts
// Pattern: Listeners subscribe to state changes and are notified on updates
const listeners = new Set<Listener>()

const subscribe = (listener: Listener) => {
  listeners.add(listener)
  return () => listeners.delete(listener)
}

// Notification happens when setState is called
listeners.forEach((listener) => listener(state, previousState))
```

#### **Higher-Order Function Pattern (Middleware)**
Middlewares wrap the store creation function to enhance functionality:

```typescript
// Located in: src/middleware/*.ts
// Pattern: Function composition for extensible behavior
// Example structure:
const middleware = (createStoreFn) => (initializer) => {
  // Pre-processing
  const store = createStoreFn(enhancedInitializer)
  // Post-processing / store augmentation
  return store
}
```

#### **Factory Pattern**
Store creation uses factory functions:

```typescript
// Located in: src/vanilla.ts - createStore
// Located in: src/react.ts - create
// Pattern: Functions that create and return configured store instances
```

#### **Closure Pattern**
State encapsulation through closures:

```typescript
// Located in: src/vanilla.ts
// Pattern: Private state accessible only through exposed methods
const createStoreImpl = (createState) => {
  let state: TState  // Private, encapsulated state
  
  const getState = () => state
  const setState = (partial, replace) => { /* mutate state */ }
  // state variable is captured in closure
}
```

---

### 3. Data Structures

#### **Listener Set**
```typescript
// Located in: src/vanilla.ts
// Purpose: Efficient O(1) add/remove for subscription management
const listeners = new Set<Listener>()
```

#### **State Container**
```typescript
// Located in: src/vanilla.ts
// Purpose: Single mutable variable holding current state
let state: TState
```

#### **Shallow Comparison Implementation**
```typescript
// Located in: src/vanilla/shallow.ts
// Purpose: Efficient object comparison for selector optimization
// Handles: Objects, Arrays, Maps, Sets, Date objects

export function shallow<T>(objA: T, objB: T): boolean {
  if (Object.is(objA, objB)) return true
  
  // Type-specific comparisons for Map, Set, Date
  if (objA instanceof Map && objB instanceof Map) {
    // Size check + entry-by-entry comparison
  }
  if (objA instanceof Set && objB instanceof Set) {
    // Size check + item-by-item comparison  
  }
  if (objA instanceof Date && objB instanceof Date) {
    return objA.getTime() === objB.getTime()
  }
  // Object/Array shallow key comparison
}
```

---

### 4. Algorithms

#### **State Update Algorithm**
```typescript
// Located in: src/vanilla.ts - setState
// Complexity: O(n) where n = number of listeners
// Flow:
1. Receive partial state or function
2. Compute next state (functional update or merge)
3. If state changed (Object.is check):
   a. Store previous state
   b. Update current state
   c. Notify all listeners
```

#### **Shallow Equality Algorithm**
```typescript
// Located in: src/vanilla/shallow.ts
// Complexity: O(n) where n = number of keys/entries
// Optimizations:
1. Object.is for primitive/reference equality (O(1) early exit)
2. Type checks for Map/Set/Date special handling
3. Key count comparison before iteration (O(1) early exit)
4. Short-circuit on first inequality found
```

---

## Implementation Details

### 1. Core Logic

#### **Vanilla Store Implementation**
```typescript
// File: src/vanilla.ts

const createStoreImpl = <T>(createState: StateCreator<T>) => {
  type TState = ReturnType<typeof createState>
  type Listener = (state: TState, prevState: TState) => void
  
  let state: TState
  const listeners: Set<Listener> = new Set()

  const setState: StoreApi<TState>['setState'] = (partial, replace) => {
    const nextState = typeof partial === 'function' 
      ? (partial as (state: TState) => TState)(state)
      : partial
    
    if (!Object.is(nextState, state)) {
      const previousState = state
      state = (replace ?? (typeof nextState !== 'object' || nextState === null))
        ? (nextState as TState)
        : Object.assign({}, state, nextState)
      listeners.forEach((listener) => listener(state, previousState))
    }
  }

  const getState: StoreApi<TState>['getState'] = () => state
  
  const subscribe: StoreApi<TState>['subscribe'] = (listener) => {
    listeners.add(listener)
    return () => listeners.delete(listener)
  }

  const api = { setState, getState, subscribe }
  state = createState(setState, getState, api)
  return api as any
}
```

#### **React Integration**
```typescript
// File: src/react.ts

// Uses React's useSyncExternalStore for concurrent mode compatibility
import { useSyncExternalStore } from 'react'

const useStore = <TState, StateSlice>(
  api: ReadonlyStoreApi<TState>,
  selector: (state: TState) => StateSlice = identity,
) => {
  const slice = useSyncExternalStore(
    api.subscribe,
    () => selector(api.getState()),
    () => selector(api.getInitialState()),
  )
  return slice
}
```

#### **State Merging Logic**
```typescript
// Located in: src/vanilla.ts - setState
// Behavior:
// - If replace=true: direct replacement
// - If nextState is primitive/null: direct replacement  
// - Otherwise: Object.assign({}, state, nextState) - shallow merge
```

### 2. Middleware Implementations

#### **Persist Middleware**
```typescript
// File: src/middleware/persist.ts
// Features:
// - Async storage support (localStorage, AsyncStorage, etc.)
// - Partial state persistence via 'partialize' option
// - State migration between versions
// - Merge strategies (shallow, deep, custom)
// - Hydration lifecycle hooks (onRehydrateStorage)
// - Skip hydration option for SSR
```

#### **DevTools Middleware**
```typescript
// File: src/middleware/devtools.ts
// Integration: @redux-devtools/extension
// Features:
// - Action naming for state changes
// - Time-travel debugging support
// - State diff visualization
// - Multiple store instance support (name option)
```

#### **Immer Middleware**
```typescript
// File: src/middleware/immer.ts
// Integration: Immer library for immutable updates
// Behavior: Wraps setState to use Immer's produce function
```

#### **Redux Middleware**
```typescript
// File: src/middleware/redux.ts
// Provides: dispatch function with reducer pattern
// Bridge: Redux DevTools compatibility
```

#### **Subscribe With Selector Middleware**
```typescript
// File: src/middleware/subscribeWithSelector.ts
// Enhancement: Adds selector-based subscriptions to vanilla store
// Feature: Only notifies when selected slice changes
```

#### **Combine Middleware**
```typescript
// File: src/middleware/combine.ts
// Purpose: Combines initial state object with state creator
// Use case: Type inference for initial state
```

#### **SSR Safe Middleware**
```typescript
// File: src/middleware/ssrSafe.ts
// Purpose: Safe store creation for server-side rendering
```

### 3. Performance Optimizations

#### **Listener Notification Optimization**
```typescript
// Located in: src/vanilla.ts
// Optimization: Object.is check before notifying listeners
// Prevents unnecessary re-renders when state hasn't changed
if (!Object.is(nextState, state)) {
  // Only then notify listeners
}
```

#### **Shallow Equality Early Exits**
```typescript
// Located in: src/vanilla/shallow.ts
// Multiple early exit points:
if (Object.is(objA, objB)) return true  // Same reference
if (keysA.length !== keysB.length) return false  // Different key counts
// Short-circuit iteration on first mismatch
```

#### **Selective Re-rendering**
```typescript
// Located in: src/react.ts and src/traditional.ts
// Mechanism: Selectors extract only needed state
// Result: Components only re-render when their slice changes
```

---

## Code Organization

### 1. Directory Structure

```
zustand/
├── src/                          # Source code
│   ├── index.ts                  # Main entry point
│   ├── vanilla.ts                # Core store (no React)
│   ├── react.ts                  # React bindings
│   ├── traditional.ts            # Legacy API with equality fn
│   ├── shallow.ts                # Re-export from vanilla/shallow
│   ├── types.d.ts                # TypeScript declarations
│   ├── middleware.ts             # Middleware re-exports
│   ├── middleware/               # Middleware implementations
│   │   ├── combine.ts
│   │   ├── devtools.ts
│   │   ├── immer.ts
│   │   ├── persist.ts
│   │   ├── redux.ts
│   │   ├── ssrSafe.ts
│   │   └── subscribeWithSelector.ts
│   ├── vanilla/                  # Vanilla-specific utilities
│   │   └── shallow.ts
│   └── react/                    # React-specific utilities
│       └── shallow.ts
├── tests/                        # Test files
│   ├── vanilla/                  # Vanilla store tests
│   └── *.test.tsx               # React integration tests
├── docs/                         # Documentation
│   ├── apis/                     # API documentation
│   ├── guides/                   # Usage guides
│   ├── middlewares/              # Middleware docs
│   └── migrations/               # Migration guides
└── examples/                     # Example applications
    ├── demo/                     # Interactive demo
    └── starter/                  # Starter template
```

### 2. Build System

#### **Build Tools**
```javascript
// File: rollup.config.mjs
// Bundler: Rollup
// Plugins:
// - @rollup/plugin-alias        - Module aliasing
// - @rollup/plugin-node-resolve - Node module resolution
// - @rollup/plugin-replace      - String replacement
// - @rollup/plugin-typescript   - TypeScript compilation
// - rollup-plugin-esbuild       - Fast minification
```

#### **Output Formats**
```javascript
// Configured in: rollup.config.mjs
// Formats produced:
// - ESM (.mjs) - Modern ES modules
// - CJS (.js) - CommonJS for Node
// - Type declarations (.d.ts)
```

#### **Package Exports**
```json
// File: package.json
// Multiple entry points:
{
  "exports": {
    ".": { "import": "./esm/index.mjs", "require": "./index.js" },
    "./vanilla": { /* vanilla entry */ },
    "./react": { /* react entry */ },
    "./middleware": { /* middleware entry */ },
    "./shallow": { /* shallow entry */ }
  }
}
```

---

## Quality Assurance

### 1. Testing Strategy

#### **Test Framework**
```typescript
// File: vitest.config.mts
// Framework: Vitest
// Environment: jsdom (for React testing)
// Coverage: @vitest/coverage-v8
```

#### **Test Categories**

| Test File | Coverage Area |
|-----------|---------------|
| `basic.test.tsx` | Core store functionality with React |
| `vanilla/basic.test.ts` | Vanilla store without React |
| `shallow.test.tsx` | Shallow comparison |
| `subscribe.test.tsx` | Subscription behavior |
| `persistSync.test.tsx` | Synchronous persist middleware |
| `persistAsync.test.tsx` | Asynchronous persist middleware |
| `devtools.test.tsx` | DevTools integration |
| `middlewareTypes.test.tsx` | Middleware TypeScript types |
| `ssr.test.tsx` | Server-side rendering |
| `types.test.tsx` | TypeScript type inference |

#### **Test Utilities**
```typescript
// File: tests/test-utils.ts
// File: tests/setup.ts
// Provides: Common testing helpers and setup
```

### 2. Test Infrastructure

```javascript
// Testing Libraries (from package.json devDependencies):
// - vitest                      - Test runner
// - @testing-library/react      - React component testing
// - @testing-library/jest-dom   - DOM assertions
// - jsdom                       - Browser environment simulation
// - @vitest/coverage-v8         - Code coverage
// - @vitest/ui                  - Test UI
```

### 3. Code Quality

#### **Linting**
```javascript
// File: eslint.config.mjs
// Plugins:
// - @eslint/js
// - typescript-eslint
// - eslint-plugin-react
// - eslint-plugin-react-hooks
// - eslint-plugin-import
// - eslint-plugin-jest-dom
// - eslint-plugin-testing-library
```

#### **Formatting**
```
// File: .prettierignore
// Tool: Prettier (from devDependencies)
```

#### **TypeScript Configuration**
```json
// File: tsconfig.json
// Strict mode for type safety
```

---

## Cross-cutting Concerns

### 1. Error Handling

#### **Development Warnings**
```typescript
// Located in: various middleware files
// Pattern: Conditional warnings in development mode
if (process.env.NODE_ENV !== 'production') {
  console.warn('[zustand] Warning message')
}
```

#### **Graceful Degradation**
```typescript
// Located in: src/middleware/persist.ts
// Behavior: Handles storage failures gracefully
// - Storage unavailable → continues without persistence
// - Deserialization errors → falls back to initial state
```

### 2. Configuration

#### **Middleware Options**
```typescript
// persist middleware options:
interface PersistOptions {
  name: string                    // Storage key
  storage?: StateStorage          // Custom storage
  partialize?: (state) => partial // Partial persistence
  version?: number                // Schema version
  migrate?: MigrateFn             // Migration function
  merge?: MergeFn                 // Custom merge strategy
  skipHydration?: boolean         // SSR support
  onRehydrateStorage?: Fn         // Lifecycle hook
}

// devtools middleware options:
interface DevtoolsOptions {
  name?: string                   // Store name
  enabled?: boolean               // Enable/disable
  anonymousActionType?: string    // Default action name
  store?: string                  // Store identifier
}
```

### 3. Platform Compatibility

#### **React Version Support**
```typescript
// File: src/react.ts
// Uses: useSyncExternalStore (React 18+)
// Polyfill: use-sync-external-store package (peer dependency)
```

#### **SSR Support**
```typescript
// File: src/middleware/ssrSafe.ts
// Mechanism: Safe store creation for server-side rendering
// Pattern: Prevents hydration mismatches
```

---

## Summary

Zustand's architecture demonstrates:

1. **Minimal Core**: ~50 lines for vanilla store implementation
2. **Functional Composition**: Middleware enhances stores through function wrapping
3. **Framework Agnostic**: Core vanilla module has zero dependencies
4. **Type Safety**: Full TypeScript support with sophisticated generics
5. **Performance Focus**: Shallow equality, selective subscriptions, early exits
6. **Modern React**: Uses `useSyncExternalStore` for concurrent mode compatibility
7. **Extensibility**: Clean middleware API for community extensions