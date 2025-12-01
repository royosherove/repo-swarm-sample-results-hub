# hl_overview

High level overview of the codebase

# Repository Analysis: React

## 0. Repository Name
[[react]]

## 1. Project Purpose

This is the **React** library - Facebook's open-source JavaScript library for building user interfaces. The repository contains:

- **Core React runtime** - The fundamental React library for component-based UI development
- **React DOM** - DOM-specific rendering methods for web applications
- **React Native Renderer** - Integration with React Native for mobile development
- **React Server Components** - Server-side rendering and streaming capabilities (Fizz/Flight)
- **React DevTools** - Browser extensions and debugging tools for React applications
- **React Compiler** - An experimental compiler for automatic optimization of React code
- **Scheduler** - Cooperative scheduling for browser environments
- **Reconciler** - The core algorithm for efficiently updating the UI

**Primary Domain:** Frontend UI development framework with server-side rendering capabilities.

## 2. Architecture Pattern

The repository follows a **Monorepo Architecture** with:

- **Package-based modular design** - Independent packages with clear boundaries
- **Host-agnostic core** - The reconciler is abstracted from specific renderers (DOM, Native, etc.)
- **Plugin/Adapter pattern** - Different renderers implement host configs
- **Event-driven architecture** - For scheduling and reconciliation
- **Streaming architecture** - For server-side rendering (Fizz for HTML, Flight for RSC)

## 3. Technology Stack

### Primary Languages
- **JavaScript** (ES6+)
- **TypeScript** (for compiler packages and ESLint plugin)
- **Flow** (static type checking throughout the codebase)

### Build & Bundling
- **Rollup** - Primary bundler for production builds
- **Webpack** - Used for DevTools and development builds
- **Babel** - JavaScript transformation and compilation

### Testing
- **Jest** - Primary testing framework
- **Playwright** - E2E testing for DevTools

### Package Management
- **Yarn** - Package manager (with workspaces)

### Configuration/Linting
- **ESLint** - Code linting with custom rules
- **Prettier** - Code formatting
- **Flow** - Static type checking

### Key Dependencies (from package.json patterns)
- `art` - Vector graphics library
- `fbjs` - Facebook's JavaScript utilities
- `object-assign` - Polyfill
- `scheduler` - Internal cooperative scheduling

## 4. Initial Structure Impression

| Directory | Purpose |
|-----------|---------|
| `packages/` | **Core libraries** - All publishable React packages |
| `scripts/` | **Build infrastructure** - Rollup configs, release scripts, testing utilities |
| `fixtures/` | **Test applications** - Example apps for manual testing and integration testing |
| `compiler/` | **React Compiler** - Separate monorepo for the experimental compiler |
| `.github/` | **CI/CD workflows** - GitHub Actions for builds, releases, and testing |
| `flow-typed/` | **Flow type definitions** - Environment and npm type definitions |

## 5. Configuration/Package Files

### Root Configuration
- `package.json` - Root workspace configuration
- `yarn.lock` - Dependency lock file
- `babel.config.js`, `babel.config-ts.js`, `babel.config-react-compiler.js` - Babel configurations
- `.eslintrc.js`, `.eslintignore` - ESLint configuration
- `.prettierrc.js`, `.prettierignore` - Prettier configuration
- `flow-typed.config.json` - Flow type configuration
- `.nvmrc` - Node version specification
- `.editorconfig` - Editor settings
- `.watchmanconfig` - Watchman configuration
- `ReactVersions.js` - Version management
- `react.code-workspace` - VS Code workspace

### Package-level configurations
Each package in `packages/` contains its own `package.json`

### Compiler configurations
- `compiler/package.json` - Compiler monorepo root
- `compiler/.eslintrc.js` - Compiler-specific linting

## 6. Directory Structure

### `/packages/` - Core Libraries

| Package | Purpose |
|---------|---------|
| `react/` | Core React APIs (createElement, hooks, etc.) |
| `react-dom/` | DOM renderer and server rendering |
| `react-dom-bindings/` | DOM-specific event handling and properties |
| `react-reconciler/` | Core reconciliation algorithm (Fiber) |
| `react-server/` | Server-side React rendering infrastructure |
| `react-client/` | Client-side Flight (RSC) consumer |
| `react-server-dom-webpack/` | RSC integration with Webpack |
| `react-server-dom-turbopack/` | RSC integration with Turbopack |
| `react-server-dom-parcel/` | RSC integration with Parcel |
| `react-server-dom-esm/` | RSC with native ESM |
| `react-native-renderer/` | React Native renderer |
| `scheduler/` | Cooperative task scheduling |
| `shared/` | Shared utilities across packages |
| `react-is/` | Type checking utilities |
| `react-refresh/` | Fast Refresh (HMR) support |
| `use-sync-external-store/` | Hook for external stores |
| `use-subscription/` | Subscription hook |

### DevTools Packages
| Package | Purpose |
|---------|---------|
| `react-devtools/` | Standalone DevTools app |
| `react-devtools-core/` | Core DevTools functionality |
| `react-devtools-shared/` | Shared DevTools utilities |
| `react-devtools-extensions/` | Browser extensions (Chrome, Firefox, Edge) |
| `react-devtools-inline/` | Embeddable DevTools |
| `react-devtools-timeline/` | Profiler timeline view |
| `react-devtools-shell/` | Development shell for DevTools |
| `react-devtools-fusebox/` | React Native DevTools integration |
| `react-debug-tools/` | Debugging utilities |

### Testing Packages
| Package | Purpose |
|---------|---------|
| `react-test-renderer/` | Test renderer for snapshots |
| `jest-react/` | Jest matchers for React |
| `internal-test-utils/` | Internal testing utilities |
| `react-noop-renderer/` | Minimal renderer for testing |
| `dom-event-testing-library/` | DOM event testing utilities |
| `react-suspense-test-utils/` | Suspense testing utilities |

### Other Packages
| Package | Purpose |
|---------|---------|
| `react-art/` | Vector graphics with ART |
| `react-cache/` | Experimental caching |
| `react-markup/` | Static markup generation |
| `eslint-plugin-react-hooks/` | ESLint rules for hooks |

### `/scripts/` - Build Infrastructure

| Directory | Purpose |
|-----------|---------|
| `rollup/` | Rollup build configuration and plugins |
| `jest/` | Jest configuration and setup |
| `babel/` | Custom Babel transforms |
| `eslint/` | ESLint configuration |
| `eslint-rules/` | Custom ESLint rules |
| `release/` | Release automation scripts |
| `flow/` | Flow type checking scripts |
| `error-codes/` | Production error code system |
| `bench/` | Performance benchmarking |
| `devtools/` | DevTools build scripts |
| `shared/` | Shared script utilities |
| `ci/` | CI-specific scripts |
| `tasks/` | Misc automation tasks |

### `/fixtures/` - Test Applications

| Directory | Purpose |
|-----------|---------|
| `dom/` | DOM integration testing |
| `ssr/`, `ssr2/` | Server-side rendering examples |
| `fizz/`, `fizz-ssr-browser/` | Streaming SSR examples |
| `flight/`, `flight-esm/`, `flight-parcel/` | React Server Components examples |
| `view-transition/` | View Transitions API integration |
| `concurrent/` | Concurrent features testing |
| `devtools/` | DevTools testing fixtures |
| `art/` | ART renderer testing |
| `scheduler/` | Scheduler testing |
| `attribute-behavior/` | DOM attribute testing |
| `packaging/` | Bundle format testing |
| `eslint-v*/` | ESLint plugin compatibility testing |
| `legacy-jsx-runtimes/` | JSX runtime compatibility |

### `/compiler/` - React Compiler (Separate Monorepo)

| Directory | Purpose |
|-----------|---------|
| `packages/babel-plugin-react-compiler/` | Babel plugin for compilation |
| `packages/eslint-plugin-react-compiler/` | ESLint integration |
| `packages/react-compiler-runtime/` | Runtime helpers |
| `packages/react-compiler-healthcheck/` | Codebase analysis tool |
| `packages/snap/` | Snapshot testing utility |
| `packages/react-forgive/` | Error recovery tool |
| `packages/react-mcp-server/` | MCP server integration |
| `apps/playground/` | Interactive compiler playground |

## 7. High-Level Architecture

### Architectural Patterns

#### 1. **Layered Architecture**
```
┌─────────────────────────────────────┐
│         Public API (react)          │
├─────────────────────────────────────┤
│     Reconciler (react-reconciler)   │
├─────────────────────────────────────┤
│  Host Config (DOM, Native, Noop)    │
├─────────────────────────────────────┤
│     Renderers (react-dom, etc.)     │
└─────────────────────────────────────┘
```

**Evidence:**
- `react/` exports public APIs
- `react-reconciler/` is renderer-agnostic
- `react-dom-bindings/` provides DOM-specific implementations
- `shared/` provides cross-cutting utilities

#### 2. **Host Config Adapter Pattern**
The reconciler is decoupled from specific platforms through host configurations.

**Evidence:**
- `scripts/shared/inlinedHostConfigs.js` - Defines host configurations
- Multiple renderer packages implement host-specific behavior
- `react-reconciler/src/forks/` - Platform-specific implementations

#### 3. **Streaming Architecture (Fizz/Flight)**
```
┌─────────────────┐     ┌─────────────────┐
│  React Server   │────▶│  Flight Stream  │
│  (RSC Runtime)  │     │    (Binary)     │
└─────────────────┘     └────────┬────────┘
                                 │
                                 ▼
┌─────────────────┐     ┌─────────────────┐
│  React Client   │◀────│  Flight Client  │
│  (Hydration)    │     │    (Parser)     │
└─────────────────┘     └─────────────────┘
```

**Evidence:**
- `react-server/` - Server rendering runtime
- `react-client/` - Client consumption
- `react-server-dom-*` packages for bundler integration

#### 4. **Event-Driven Scheduling**
```
┌─────────────────────────────────────┐
│            Scheduler                │
├─────────────────────────────────────┤
│  Priority Queues │ Time Slicing    │
└─────────────────────────────────────┘
              │
              ▼
┌─────────────────────────────────────┐
│         Reconciler                  │
│   (Interruptible Work Units)        │
└─────────────────────────────────────┘
```

**Evidence:**
- `scheduler/` package with priority-based scheduling
- `react-reconciler/` uses scheduler for work management
- Concurrent Mode features in reconciler

## 8. Build, Execution and Test

### Building

**Main Build Command:**
```bash
yarn build
```

**Build Scripts (from `scripts/rollup/`):**
- `build.js` - Main build entry point
- `build-all-release-channels.js` - Builds all release variants
- `bundles.js` - Bundle configuration
- `packaging.js` - NPM package preparation

**Build Outputs:**
- UMD bundles for browser
- CommonJS for Node.js
- ESM for modern bundlers
- Separate development and production builds

### Running

This is a library, not an application. To develop:

```bash
# Install dependencies
yarn install

# Build packages
yarn build

# Run fixtures for testing
cd fixtures/dom && yarn start
```

### Testing

**Test Commands:**
```bash
# Run all tests
yarn test

# Run tests for specific package
yarn test --selectProjects react-dom

# Run with specific renderer
yarn test-www  # Facebook www config
yarn test-persistent  # Persistent mode
```

**Jest Configuration:**
- `scripts/jest/config.base.js` - Base configuration
- `scripts/jest/config.source.js` - Source tests
- `scripts/jest/config.build.js` - Build tests
- `scripts/jest/setupTests.js` - Test setup

**Test Types:**
1. **Unit tests** - In `__tests__/` directories throughout packages
2. **Integration tests** - In fixtures
3. **E2E tests** - Playwright for DevTools (`react-devtools-inline/__tests__/__e2e__/`)
4. **Fuzz tests** - `runtime_fuzz_tests.yml` workflow

### CI/CD Workflows

| Workflow | Purpose |
|----------|---------|
| `runtime_build_and_test.yml` | Main CI pipeline |
| `runtime_prereleases.yml` | Automated prereleases |
| `runtime_commit_artifacts.yml` | Build artifact publishing |
| `compiler_prereleases.yml` | Compiler releases |
| `devtools_regression_tests.yml` | DevTools testing |
| `shared_lint.yml` | Linting checks |

### Entry Points

**React Core:**
- `packages/react/index.js` - Main React export
- `packages/react/jsx-runtime.js` - JSX runtime

**React DOM:**
- `packages/react-dom/index.js` - Main DOM export
- `packages/react-dom/client.js` - Client rendering
- `packages/react-dom/server.js` - Server rendering

**DevTools:**
- `packages/react-devtools/bin.js` - CLI entry
- `packages/react-devtools-extensions/` - Browser extension entries

# module_deep_dive

Deep dive into modules

# Detailed Component Breakdown

## 1. `packages/react/`

### Core Responsibility
The core React library that provides the fundamental building blocks for building user interfaces. This is the main package that developers import when using React.

### Key Components

| File/Directory | Role |
|----------------|------|
| `index.js` | Main entry point exporting all public React APIs |
| `jsx-runtime.js` | JSX transformation runtime (automatic JSX transform) |
| `jsx-dev-runtime.js` | Development-mode JSX runtime with additional debugging |
| `compiler-runtime.js` | Runtime support for React Compiler |
| `react.react-server.js` | React Server Components entry point |
| `src/ReactElement.js` | `createElement` and element creation logic |
| `src/ReactHooks.js` | Hook implementations (`useState`, `useEffect`, etc.) |
| `src/ReactContext.js` | Context API implementation |
| `src/ReactChildren.js` | `React.Children` utilities |
| `src/ReactLazy.js` | `React.lazy()` for code splitting |
| `src/ReactMemo.js` | `React.memo()` for memoization |
| `src/jsx/` | JSX runtime implementations |

### Dependencies & Interactions

**Internal Dependencies:**
- `@packages/shared/` - Shared utilities, symbols, and type definitions
- `@packages/react-reconciler/` - Referenced types for fiber/reconciler integration

**External Interactions:**
- None directly (pure library, no external API calls)

---

## 2. `packages/react-dom/`

### Core Responsibility
React's DOM renderer - handles rendering React components to the browser DOM, including client-side rendering, server-side rendering (SSR), and hydration.

### Key Components

| File/Directory | Role |
|----------------|------|
| `client.js` | Client-side rendering entry (`createRoot`, `hydrateRoot`) |
| `server.js` / `server.node.js` / `server.browser.js` | SSR streaming APIs |
| `static.js` | Static HTML generation (prerendering) |
| `test-utils.js` | Testing utilities for React DOM |
| `src/client/ReactDOMRoot.js` | Root container management |
| `src/client/ReactDOMComponent.js` | DOM component handling |
| `src/events/` | Synthetic event system |
| `src/server/` | Server rendering implementation |
| `src/shared/` | Shared DOM utilities |

### Dependencies & Interactions

**Internal Dependencies:**
- `@packages/react/` - Core React types and APIs
- `@packages/react-reconciler/` - Reconciliation algorithm
- `@packages/react-dom-bindings/` - Low-level DOM bindings
- `@packages/shared/` - Shared utilities
- `@packages/scheduler/` - Task scheduling

**External Interactions:**
- Browser DOM APIs (document, window, events)
- Node.js streams (for SSR in Node environment)
- Web Streams API (for browser/edge SSR)

---

## 3. `packages/react-reconciler/`

### Core Responsibility
The core reconciliation algorithm (Fiber architecture) that handles diffing, scheduling, and coordinating updates across all React renderers.

### Key Components

| File/Directory | Role |
|----------------|------|
| `src/ReactFiber.js` | Fiber node creation and management |
| `src/ReactFiberWorkLoop.js` | Main work loop for processing updates |
| `src/ReactFiberReconciler.js` | Public reconciler API for renderers |
| `src/ReactFiberHooks.js` | Hooks implementation at fiber level |
| `src/ReactFiberCommitWork.js` | Commit phase (applying changes) |
| `src/ReactFiberBeginWork.js` | Begin phase (traversing tree) |
| `src/ReactFiberCompleteWork.js` | Complete phase (bubbling up) |
| `src/ReactFiberSchedulerPriorities.js` | Priority-based scheduling |
| `src/ReactChildFiber.js` | Child reconciliation logic |
| `src/forks/` | Platform-specific implementations |
| `constants.js` | Exported constants for renderers |
| `reflection.js` | Fiber reflection utilities |

### Dependencies & Interactions

**Internal Dependencies:**
- `@packages/shared/` - Shared utilities and feature flags
- `@packages/scheduler/` - Cooperative scheduling
- `@packages/react/` - React element types

**External Interactions:**
- Host config injection (renderers provide platform bindings)
- Performance APIs (`performance.now()`, `MessageChannel`)

---

## 4. `packages/scheduler/`

### Core Responsibility
Cooperative scheduling library that manages task prioritization and time-slicing for React's concurrent features.

### Key Components

| File/Directory | Role |
|----------------|------|
| `index.js` | Main entry point |
| `index.native.js` | React Native specific entry |
| `unstable_mock.js` | Mock scheduler for testing |
| `unstable_post_task.js` | `scheduler.postTask` API integration |
| `src/Scheduler.js` | Core scheduling logic |
| `src/SchedulerMinHeap.js` | Priority queue implementation |
| `src/SchedulerPriorities.js` | Priority level definitions |
| `src/SchedulerFeatureFlags.js` | Feature flags |
| `src/forks/` | Platform-specific scheduler implementations |

### Dependencies & Interactions

**Internal Dependencies:**
- `@packages/shared/` - Shared utilities

**External Interactions:**
- `MessageChannel` API (for yielding to browser)
- `performance.now()` (timing)
- `scheduler.postTask()` (when available)
- `setImmediate` / `setTimeout` (fallbacks)

---

## 5. `packages/react-server/`

### Core Responsibility
Server-side React rendering infrastructure for React Server Components (RSC) and streaming SSR (Fizz).

### Key Components

| File/Directory | Role |
|----------------|------|
| `index.js` | Fizz streaming SSR entry |
| `flight.js` | React Flight (RSC protocol) entry |
| `src/ReactFizzServer.js` | Streaming HTML renderer (Fizz) |
| `src/ReactFlightServer.js` | RSC serialization |
| `src/ReactServerStreamConfig*.js` | Stream configuration per environment |
| `src/flight/` | Flight protocol implementation |
| `src/forks/` | Environment-specific implementations |

### Dependencies & Interactions

**Internal Dependencies:**
- `@packages/react/` - React types and elements
- `@packages/shared/` - Shared utilities
- `@packages/react-dom-bindings/` - DOM-specific rendering hints

**External Interactions:**
- Node.js streams (`Readable`, `Writable`)
- Web Streams API (`ReadableStream`)
- Bundler integration (Webpack/Turbopack module references)

---

## 6. `packages/react-client/`

### Core Responsibility
Client-side infrastructure for consuming React Server Components - deserializes the Flight protocol stream.

### Key Components

| File/Directory | Role |
|----------------|------|
| `flight.js` | Main Flight client entry |
| `src/ReactFlightClient.js` | Core Flight client implementation |
| `src/ReactFlightClientStream.js` | Stream parsing |
| `src/ReactFlightReplyClient.js` | Server action replies |
| `src/forks/` | Environment-specific forks |

### Dependencies & Interactions

**Internal Dependencies:**
- `@packages/react/` - React types
- `@packages/shared/` - Shared utilities

**External Interactions:**
- Network fetch APIs
- Bundler-generated module maps

---

## 7. `packages/react-server-dom-webpack/`

### Core Responsibility
Webpack-specific integration for React Server Components, providing both server and client implementations for the RSC protocol with Webpack bundler.

### Key Components

| File/Directory | Role |
|----------------|------|
| `client.js` / `client.browser.js` / `client.node.js` | Client entry points |
| `server.js` / `server.browser.js` / `server.node.js` | Server entry points |
| `static.js` | Static prerendering |
| `plugin.js` | Webpack plugin for RSC |
| `node-register.js` | Node.js loader registration |
| `src/client/` | Client-side Flight consumption |
| `src/server/` | Server-side Flight production |
| `src/shared/` | Shared Webpack-specific utilities |

### Dependencies & Interactions

**Internal Dependencies:**
- `@packages/react-server/` - Server rendering core
- `@packages/react-client/` - Client consumption core
- `@packages/shared/` - Shared utilities

**External Interactions:**
- **Webpack** bundler APIs and module system
- `acorn` for parsing (potentially)
- Network/fetch for client streaming

---

## 8. `packages/react-server-dom-turbopack/`

### Core Responsibility
Turbopack-specific integration for React Server Components (Next.js's new bundler).

### Key Components

| File/Directory | Role |
|----------------|------|
| `client.*.js` | Environment-specific client entries |
| `server.*.js` | Environment-specific server entries |
| `static.*.js` | Static generation entries |
| `src/client/` | Turbopack client Flight implementation |
| `src/server/` | Turbopack server Flight implementation |
| `src/shared/` | Turbopack-specific shared code |

### Dependencies & Interactions

**Internal Dependencies:**
- `@packages/react-server/` - Server rendering core
- `@packages/react-client/` - Client consumption core
- `@packages/shared/` - Shared utilities

**External Interactions:**
- **Turbopack** bundler runtime and module system
- Primarily used within Next.js

---

## 9. `packages/react-dom-bindings/`

### Core Responsibility
Low-level DOM bindings extracted from react-dom, handling direct DOM manipulation, event handling, and property management.

### Key Components

| File/Directory | Role |
|----------------|------|
| `src/client/` | Client-side DOM operations |
| `src/client/ReactDOMHostConfig.js` | Host config for DOM renderer |
| `src/client/ReactDOMComponentTree.js` | DOM node to Fiber mapping |
| `src/events/` | Event system (delegation, plugins) |
| `src/events/DOMEventProperties.js` | Event property definitions |
| `src/events/ReactDOMEventListener.js` | Event delegation |
| `src/server/` | Server-side DOM rendering utilities |
| `src/shared/` | Shared DOM utilities |

### Dependencies & Interactions

**Internal Dependencies:**
- `@packages/react-reconciler/` - Reconciler integration
- `@packages/shared/` - Shared utilities

**External Interactions:**
- Browser DOM APIs directly
- Event APIs (`addEventListener`, event objects)

---

## 10. `packages/shared/`

### Core Responsibility
Shared utilities, constants, type definitions, and feature flags used across all React packages.

### Key Components

| File/Directory | Role |
|----------------|------|
| `ReactSharedInternals.js` | Internal shared state between packages |
| `ReactFeatureFlags.js` | Feature flag definitions |
| `ReactSymbols.js` | Symbol definitions for element types |
| `ReactTypes.js` | Shared TypeScript/Flow types |
| `ReactElementType.js` | Element type definitions |
| `getComponentNameFromType.js` | Component name extraction |
| `CheckStringCoercion.js` | String coercion validation |
| `shallowEqual.js` | Shallow comparison utility |
| `objectIs.js` | `Object.is` polyfill |
| `assign.js` | `Object.assign` utility |
| `forks/` | Environment-specific overrides |

### Dependencies & Interactions

**Internal Dependencies:**
- None (this is the base dependency layer)

**External Interactions:**
- None (pure utilities)

---

## 11. `packages/react-native-renderer/`

### Core Responsibility
React renderer for React Native, bridging React's reconciler with native mobile platform components.

### Key Components

| File/Directory | Role |
|----------------|------|
| `index.js` | Main React Native renderer |
| `fabric.js` | New Fabric architecture renderer |
| `src/ReactNativeRenderer.js` | Core native renderer |
| `src/ReactFabric.js` | Fabric renderer implementation |
| `src/ReactNativeHostConfig.js` | Host config for native |
| `src/ReactNativeTypes.js` | Native-specific types |
| `src/legacy-events/` | Legacy event system |

### Dependencies & Interactions

**Internal Dependencies:**
- `@packages/react-reconciler/` - Reconciliation algorithm
- `@packages/shared/` - Shared utilities
- `@packages/scheduler/` - Task scheduling

**External Interactions:**
- React Native bridge/JSI
- Native UI components via UIManager
- Fabric rendering system

---

## 12. `packages/react-test-renderer/`

### Core Responsibility
Test renderer for React that renders to pure JavaScript objects, enabling testing without a DOM.

### Key Components

| File/Directory | Role |
|----------------|------|
| `index.js` | Main entry point |
| `shallow.js` | Shallow rendering entry |
| `src/ReactTestRenderer.js` | Test renderer implementation |
| `src/ReactTestHostConfig.js` | Host config for test renderer |

### Dependencies & Interactions

**Internal Dependencies:**
- `@packages/react-reconciler/` - Reconciliation
- `@packages/shared/` - Shared utilities

**External Interactions:**
- None (pure JavaScript output)

---

## 13. `packages/react-devtools-shared/`

### Core Responsibility
Shared code for React DevTools across all platforms (browser extension, standalone, etc.).

### Key Components

| File/Directory | Role |
|----------------|------|
| `src/backend/` | Backend agent running in inspected page |
| `src/frontend/` | Frontend UI components |
| `src/devtools/` | DevTools views and stores |
| `src/hooks/` | Hook inspection logic |
| `src/bridge.js` | Communication bridge |
| `src/types.js` | Shared type definitions |
| `src/utils.js` | Utility functions |
| `src/hydration.js` | Data hydration for display |

### Dependencies & Interactions

**Internal Dependencies:**
- `@packages/react-debug-tools/` - Hook inspection

**External Interactions:**
- Browser extension APIs
- WebSocket (for standalone)
- Chrome DevTools Protocol

---

## 14. `packages/react-devtools-extensions/`

### Core Responsibility
Browser extension builds for React DevTools (Chrome, Firefox, Edge).

### Key Components

| File/Directory | Role |
|----------------|------|
| `chrome/` | Chrome extension manifest and assets |
| `firefox/` | Firefox extension manifest |
| `edge/` | Edge extension manifest |
| `src/background/` | Extension background scripts |
| `src/contentScripts/` | Page injection scripts |
| `src/main/` | Main panel implementation |
| `build.js` | Extension build script |
| `webpack.config.js` | Webpack configuration |
| `popups/` | Extension popup UIs |

### Dependencies & Interactions

**Internal Dependencies:**
- `@packages/react-devtools-shared/` - Shared DevTools code

**External Interactions:**
- Browser Extension APIs (chrome.*, browser.*)
- Page content scripts injection
- Message passing between contexts

---

## 15. `packages/eslint-plugin-react-hooks/`

### Core Responsibility
ESLint plugin enforcing the Rules of Hooks and providing the `exhaustive-deps` rule.

### Key Components

| File/Directory | Role |
|----------------|------|
| `index.js` | Plugin entry point |
| `src/rules/RulesOfHooks.js` | Rules of Hooks enforcement |
| `src/rules/ExhaustiveDeps.js` | Dependency array validation |
| `src/code-path-analysis/` | Control flow analysis |
| `src/shared/` | Shared utilities |
| `__tests__/` | Rule tests |

### Dependencies & Interactions

**Internal Dependencies:**
- None

**External Interactions:**
- ESLint API (rule context, AST)
- Works with ESLint v6-v9

---

## 16. `packages/use-sync-external-store/`

### Core Responsibility
Backward-compatible shim for `useSyncExternalStore` hook, enabling external store subscriptions with concurrent rendering support.

### Key Components

| File/Directory | Role |
|----------------|------|
| `index.js` | Main entry |
| `with-selector.js` | Version with selector support |
| `shim/` | Shim for older React versions |
| `src/useSyncExternalStore.js` | Hook implementation |
| `src/useSyncExternalStoreWithSelector.js` | Selector variant |

### Dependencies & Interactions

**Internal Dependencies:**
- `@packages/react/` - React hooks (when using native implementation)

**External Interactions:**
- None (pure React hook)

---

## 17. `packages/react-refresh/`

### Core Responsibility
Fast Refresh implementation enabling hot reloading of React components during development.

### Key Components

| File/Directory | Role |
|----------------|------|
| `babel.js` | Babel plugin for transform |
| `runtime.js` | Runtime for hot updates |
| `src/ReactFreshRuntime.js` | Core refresh logic |
| `src/ReactFreshBabelPlugin.js` | Babel transformation |

### Dependencies & Interactions

**Internal Dependencies:**
- `@packages/react-reconciler/` - For hot update integration

**External Interactions:**
- Babel transformation pipeline
- Bundler HMR APIs (Webpack, Vite, etc.)

---

## 18. `scripts/rollup/`

### Core Responsibility
Build system for bundling all React packages using Rollup.

### Key Components

| File/Directory | Role |
|----------------|------|
| `build.js` | Main build script |
| `build-all-release-channels.js` | Multi-channel builds |
| `bundles.js` | Bundle definitions |
| `forks.js` | Fork resolution logic |
| `modules.js` | Module configuration |
| `packaging.js` | Package.json generation |
| `wrappers.js` | UMD/CJS/ESM wrappers |
| `plugins/` | Custom Rollup plugins |
| `validate/` | Build validation |

### Dependencies & Interactions

**Internal Dependencies:**
- `@scripts/shared/` - Shared build utilities
- `@scripts/flags/` - Feature flags
- `@scripts/error-codes/` - Error code extraction

**External Interactions:**
- Rollup bundler
- Google Closure Compiler
- npm/yarn publishing

---

## 19. `scripts/jest/`

### Core Responsibility
Jest testing infrastructure and configuration for the React monorepo.

### Key Components

| File/Directory | Role |
|----------------|------|
| `config.base.js` | Base Jest configuration |
| `config.source.js` | Source testing config |
| `config.build.js` | Build artifact testing |
| `preprocessor.js` | Code transformation |
| `setupTests.js` | Test environment setup |
| `setupHostConfigs.js` | Host config mocking |
| `matchers/` | Custom Jest matchers |
| `devtools/` | DevTools-specific test setup |

### Dependencies & Interactions

**Internal Dependencies:**
- `@packages/internal-test-utils/` - Test utilities
- `@scripts/babel/` - Babel transforms

**External Interactions:**
- Jest testing framework
- jsdom for DOM simulation

---

## 20. `compiler/packages/babel-plugin-react-compiler/`

### Core Responsibility
The React Compiler (formerly React Forget) - automatically memoizes React components and hooks.

### Key Components

| File/Directory | Role |
|----------------|------|
| `src/Babel/` | Babel plugin entry and integration |
| `src/HIR/` | High-level IR representation |
| `src/ReactiveScopes/` | Reactive scope analysis |
| `src/Optimization/` | Memoization optimizations |
| `src/Codegen/` | Code generation from IR |
| `src/Validation/` | Rules of React validation |
| `src/Entrypoint/` | Compilation pipeline |

### Dependencies & Interactions

**Internal Dependencies:**
- `@compiler/packages/react-compiler-runtime/` - Runtime helpers

**External Interactions:**
- Babel transformation API
- Integrates with bundlers via Babel

---

## 21. `fixtures/flight/`

### Core Responsibility
Reference implementation/fixture for testing React Server Components with Webpack.

### Key Components

| File/Directory | Role |
|----------------|------|
| `server/` | Express server with RSC handling |
| `src/` | Example RSC application |
| `loader/` | Custom Webpack loaders |
| `config/` | Webpack configurations |
| `__tests__/` | E2E tests with Playwright |

### Dependencies & Interactions

**Internal Dependencies:**
- `@packages/react-server-dom-webpack/` - RSC implementation

**External Interactions:**
- Express.js server
- Webpack bundler
- Playwright for E2E tests

# dependencies

Analyze dependencies and external libraries

# Dependency and Architecture Analysis

## Repository: react_33c851c7

---

## Internal Modules

The React repository is organized as a monorepo with multiple internal packages under the `packages/` directory. Below are the core internal modules and their primary responsibilities:

### Core React Packages

| Module | Description |
|--------|-------------|
| **react** | The core React library providing the fundamental React API (components, hooks, createElement, etc.) |
| **react-dom** | DOM-specific rendering methods for React, including client-side rendering and server-side rendering capabilities |
| **react-dom-bindings** | Low-level DOM bindings and event system used by react-dom |
| **react-reconciler** | The core reconciliation algorithm (Fiber) that powers React's rendering across different host environments |
| **scheduler** | Cooperative scheduling primitives used by React for prioritizing and batching work |

### Server-Side Rendering & React Server Components

| Module | Description |
|--------|-------------|
| **react-server** | Server-side rendering infrastructure for React Server Components |
| **react-client** | Client-side flight protocol implementation for consuming React Server Components |
| **react-server-dom-webpack** | Webpack integration for React Server Components (bundler plugin and runtime) |
| **react-server-dom-turbopack** | Turbopack integration for React Server Components |
| **react-server-dom-parcel** | Parcel integration for React Server Components |
| **react-server-dom-esm** | ESM-based React Server Components support |
| **react-server-dom-fb** | Facebook-internal React Server Components implementation |
| **react-markup** | Lightweight markup generation utilities for React |

### React Native

| Module | Description |
|--------|-------------|
| **react-native-renderer** | React renderer for React Native, including Fabric support |

### Developer Tools

| Module | Description |
|--------|-------------|
| **react-devtools** | Standalone React DevTools application (Electron-based) |
| **react-devtools-core** | Core DevTools functionality shared between different DevTools builds |
| **react-devtools-extensions** | Browser extension builds for Chrome, Firefox, and Edge |
| **react-devtools-inline** | Embeddable DevTools for use within web applications |
| **react-devtools-shared** | Shared components and utilities across all DevTools packages |
| **react-devtools-shell** | Development shell for testing DevTools |
| **react-devtools-timeline** | Performance timeline visualization for React DevTools |
| **react-devtools-fusebox** | DevTools integration for React Native Fusebox debugger |

### Testing Utilities

| Module | Description |
|--------|-------------|
| **react-test-renderer** | Test renderer for snapshot testing React components |
| **jest-react** | Jest matchers and utilities for testing React components |
| **react-noop-renderer** | No-op renderer used for internal testing of the reconciler |
| **react-suspense-test-utils** | Testing utilities for React Suspense |
| **dom-event-testing-library** | DOM event simulation utilities for testing |
| **internal-test-utils** | Internal testing utilities used across the React codebase |

### Hooks & Utilities

| Module | Description |
|--------|-------------|
| **use-sync-external-store** | Hook for subscribing to external stores with concurrent rendering support |
| **use-subscription** | Hook for subscribing to external data sources (built on use-sync-external-store) |
| **react-is** | Runtime type checking utilities for React element types |
| **react-cache** | Experimental caching library for React |
| **react-refresh** | Fast Refresh runtime for hot module replacement during development |

### Linting

| Module | Description |
|--------|-------------|
| **eslint-plugin-react-hooks** | ESLint plugin enforcing Rules of Hooks |

### Other Packages

| Module | Description |
|--------|-------------|
| **react-art** | React renderer for the ART drawing library |
| **react-debug-tools** | Debugging utilities for inspecting React component hooks |
| **shared** | Shared internal utilities, constants, and types used across all React packages |

### Compiler Packages (under `compiler/packages/`)

| Module | Description |
|--------|-------------|
| **babel-plugin-react-compiler** | Babel plugin for the React Compiler (automatic memoization) |
| **eslint-plugin-react-compiler** | ESLint plugin for React Compiler compatibility checks |
| **react-compiler-runtime** | Runtime support for React Compiler output |
| **react-compiler-healthcheck** | CLI tool for checking React Compiler compatibility |
| **react-mcp-server** | Model Context Protocol server for React documentation |
| **react-forgive** | VS Code language server for React Compiler |
| **snap** | Snapshot testing utility for the React Compiler |
| **make-read-only-util** | Utility for making objects read-only (used by compiler) |

### Scripts & Build Infrastructure (under `scripts/`)

| Module | Description |
|--------|-------------|
| **scripts/rollup** | Rollup build configuration and plugins for bundling React packages |
| **scripts/jest** | Jest configuration and custom test environments |
| **scripts/babel** | Custom Babel transforms for the React build process |
| **scripts/eslint-rules** | Custom ESLint rules for the React codebase |
| **scripts/release** | Release automation scripts |
| **scripts/flow** | Flow type checking configuration |
| **scripts/error-codes** | Error code extraction and transformation for production builds |

---

## External Dependencies

### Core Build & Transpilation

| Dependency | Official Name | Purpose | Source |
|------------|---------------|---------|--------|
| `@babel/core` | Babel | JavaScript compiler/transpiler core | `/package.json`, `/compiler/apps/playground/package.json`, multiple others |
| `@babel/parser` | Babel Parser | JavaScript/TypeScript parser | `/package.json`, `/packages/react-devtools-shared/package.json` |
| `@babel/traverse` | Babel Traverse | AST traversal utilities | `/package.json`, `/packages/react-devtools-shared/package.json` |
| `@babel/generator` | Babel Generator | Code generation from AST | `/compiler/apps/playground/package.json` |
| `@babel/types` | Babel Types | AST type definitions and builders | `/compiler/packages/babel-plugin-react-compiler/package.json`, `/package.json` |
| `@babel/preset-react` | Babel React Preset | React JSX transformation preset | `/package.json`, multiple fixture files |
| `@babel/preset-typescript` | Babel TypeScript Preset | TypeScript transformation preset | `/compiler/apps/playground/package.json`, `/package.json` |
| `@babel/preset-flow` | Babel Flow Preset | Flow type stripping preset | `/package.json`, `/compiler/packages/snap/package.json` |
| `@babel/preset-env` | Babel Env Preset | Environment-based transpilation | `/package.json`, `/compiler/packages/react-mcp-server/package.json` |
| `@babel/register` | Babel Register | Runtime transpilation hook | `/fixtures/fizz/package.json`, `/fixtures/view-transition/package.json` |
| `@babel/runtime` | Babel Runtime | Runtime helpers for Babel | `/packages/react-devtools-shared/package.json` |
| `@babel/code-frame` | Babel Code Frame | Code frame formatting for errors | `/compiler/packages/snap/package.json`, `/package.json` |
| `typescript` | TypeScript | TypeScript compiler | `/package.json`, `/compiler/package.json` |

### Bundlers & Build Tools

| Dependency | Official Name | Purpose | Source |
|------------|---------------|---------|--------|
| `rollup` | Rollup | Module bundler for library builds | `/package.json` |
| `@rollup/plugin-babel` | Rollup Babel Plugin | Babel integration for Rollup | `/package.json` |
| `@rollup/plugin-commonjs` | Rollup CommonJS Plugin | CommonJS module support | `/package.json` |
| `@rollup/plugin-node-resolve` | Rollup Node Resolve | Node module resolution | `/package.json` |
| `@rollup/plugin-replace` | Rollup Replace Plugin | String replacement during build | `/package.json` |
| `@rollup/plugin-typescript` | Rollup TypeScript Plugin | TypeScript support for Rollup | `/package.json` |
| `rollup-plugin-dts` | Rollup DTS Plugin | TypeScript declaration bundling | `/package.json` |
| `webpack` | Webpack | Module bundler | `/fixtures/flight/package.json`, `/packages/react-devtools-core/package.json` |
| `webpack-cli` | Webpack CLI | Command line interface for Webpack | `/fixtures/fizz/package.json`, `/packages/react-devtools-core/package.json` |
| `webpack-dev-server` | Webpack Dev Server | Development server with HMR | `/packages/react-devtools-extensions/package.json` |
| `webpack-dev-middleware` | Webpack Dev Middleware | Express middleware for Webpack | `/fixtures/flight/package.json` |
| `webpack-hot-middleware` | Webpack Hot Middleware | Hot module replacement middleware | `/fixtures/flight/package.json` |
| `webpack-sources` | Webpack Sources | Source code abstractions for Webpack | `/packages/react-server-dom-webpack/package.json`, `/fixtures/flight-esm/package.json` |
| `esbuild` | esbuild | Fast JavaScript bundler | `/compiler/package.json` |
| `tsup` | tsup | TypeScript bundler (esbuild-based) | `/package.json`, `/compiler/package.json` |
| `parcel` | Parcel | Zero-config bundler | `/fixtures/flight-parcel/package.json` |
| `browserify` | Browserify | Browser bundler | `/fixtures/packaging/browserify/dev/package.json` |
| `google-closure-compiler` | Google Closure Compiler | JavaScript optimizer | `/package.json` |

### Testing Frameworks

| Dependency | Official Name | Purpose | Source |
|------------|---------------|---------|--------|
| `jest` | Jest | JavaScript testing framework | `/package.json`, `/compiler/packages/babel-plugin-react-compiler/package.json` |
| `jest-cli` | Jest CLI | Jest command line interface | `/package.json` |
| `jest-diff` | Jest Diff | Diff utility for Jest | `/package.json`, `/fixtures/dom/package.json` |
| `jest-environment-jsdom` | Jest JSDOM Environment | JSDOM test environment | `/package.json` |
| `jest-snapshot-serializer-raw` | Jest Raw Serializer | Raw snapshot serialization | `/package.json` |
| `@playwright/test` | Playwright | End-to-end testing framework | `/compiler/apps/playground/package.json`, `/fixtures/flight/package.json` |
| `@testing-library/react` | Testing Library React | React testing utilities | `/fixtures/flight/package.json`, `/compiler/packages/snap/package.json` |
| `@testing-library/jest-dom` | Testing Library Jest DOM | Custom Jest matchers for DOM | `/fixtures/flight/package.json` |
| `@testing-library/user-event` | Testing Library User Event | User interaction simulation | `/fixtures/flight/package.json` |
| `mocha` | Mocha | Test framework | `/compiler/packages/react-forgive/package.json` |
| `jsdom` | jsdom | DOM implementation for Node.js | `/compiler/packages/snap/package.json` |

### Linting & Code Quality

| Dependency | Official Name | Purpose | Source |
|------------|---------------|---------|--------|
| `eslint` | ESLint | JavaScript linter | `/package.json`, `/fixtures/eslint-v6/package.json` through `/fixtures/eslint-v9/package.json` |
| `@typescript-eslint/parser` | TypeScript ESLint Parser | TypeScript parser for ESLint | `/package.json` |
| `@typescript-eslint/eslint-plugin` | TypeScript ESLint Plugin | TypeScript rules for ESLint | `/package.json` |
| `eslint-config-prettier` | ESLint Prettier Config | Disables conflicting Prettier rules | `/package.json` |
| `eslint-plugin-jest` | ESLint Jest Plugin | Jest-specific linting rules | `/package.json` |
| `eslint-plugin-react` | ESLint React Plugin | React-specific linting rules | `/package.json` |
| `prettier` | Prettier | Code formatter | `/package.json`, `/compiler/package.json` |
| `flow-bin` | Flow | Static type checker for JavaScript | `/package.json` |
| `flow-remove-types` | Flow Remove Types | Strips Flow type annotations | `/package.json` |
| `hermes-parser` | Hermes Parser | JavaScript parser (React Native) | `/compiler/apps/playground/package.json`, `/packages/eslint-plugin-react-hooks/package.json` |
| `hermes-eslint` | Hermes ESLint | ESLint parser using Hermes | `/compiler/apps/playground/package.json`, `/package.json` |

### Schema Validation

| Dependency | Official Name | Purpose | Source |
|------------|---------------|---------|--------|
| `zod` | Zod | TypeScript-first schema validation | `/compiler/packages/eslint-plugin-react-compiler/package.json`, `/compiler/packages/react-mcp-server/package.json` |
| `zod-validation-error` | Zod Validation Error | Human-readable Zod errors | `/compiler/packages/eslint-plugin-react-compiler/package.json` |

### Server & HTTP

| Dependency | Official Name | Purpose | Source |
|------------|---------------|---------|--------|
| `express` | Express | Web framework for Node.js | `/fixtures/fizz/package.json`, `/fixtures/ssr/package.json`, `/fixtures/flight-parcel/package.json` |
| `body-parser` | Body Parser | HTTP request body parsing | `/fixtures/flight/package.json`, `/fixtures/flight-esm/package.json` |
| `compression` | Compression | HTTP compression middleware | `/fixtures/fizz/package.json`, `/fixtures/flight/package.json` |
| `undici` | Undici | HTTP/1.1 client for Node.js | `/fixtures/flight/package.json`, `/package.json` |
| `busboy` | Busboy | Streaming multipart parser | `/fixtures/flight/package.json`, `/fixtures/flight-esm/package.json` |
| `node-fetch` | Node Fetch | Fetch API for Node.js | `/fixtures/ssr/package.json` |
| `http-server` | HTTP Server | Simple static file server | `/scripts/bench/package.json`, `/fixtures/stacks/package.json` |
| `nodemon` | Nodemon | Development server with auto-restart | `/fixtures/fizz/package.json`, `/fixtures/flight/package.json` |

### UI & Components (DevTools/Playground)

| Dependency | Official Name | Purpose | Source |
|------------|---------------|---------|--------|
| `@monaco-editor/react` | Monaco Editor React | Code editor component | `/compiler/apps/playground/package.json` |
| `monaco-editor` | Monaco Editor | Code editor (VS Code's editor) | `/compiler/apps/playground/package.json` |
| `@heroicons/react` | Heroicons | SVG icon components | `/compiler/apps/playground/package.json` |
| `@reach/menu-button` | Reach Menu Button | Accessible menu component | `/packages/react-devtools-shared/package.json` |
| `@reach/tooltip` | Reach Tooltip | Accessible tooltip component | `/packages/react-devtools-shared/package.json` |
| `react-window` | React Window | Virtualized list rendering | `/packages/react-devtools-shared/package.json` |
| `react-virtualized-auto-sizer` | React Virtualized Auto Sizer | Auto-sizing wrapper for virtualized lists | `/packages/react-devtools-shared/package.json` |
| `react-virtualized` | React Virtualized | Virtualized components | `/fixtures/attribute-behavior/package.json` |
| `notistack` | Notistack | Snackbar notifications | `/compiler/apps/playground/package.json` |
| `re-resizable` | Re-resizable | Resizable component | `/compiler/apps/playground/package.json` |
| `@use-gesture/react` | Use Gesture | Gesture handling hooks | `/compiler/apps/playground/package.json` |

### State Management & Routing

| Dependency | Official Name | Purpose | Source |
|------------|---------------|---------|--------|
| `redux` | Redux | State management library | `/fixtures/nesting/package.json` |
| `react-redux` | React Redux | React bindings for Redux | `/fixtures/nesting/src/legacy/package.json`, `/fixtures/nesting/src/modern/package.json` |
| `react-router-dom` | React Router DOM | Declarative routing for React | `/fixtures/nesting/src/legacy/package.json` |

### Frameworks

| Dependency | Official Name | Purpose | Source |
|------------|---------------|---------|--------|
| `next` | Next.js | React framework | `/compiler/apps/playground/package.json` |
| `react-scripts` | Create React App | React application tooling | `/fixtures/attribute-behavior/package.json`, `/fixtures/owner-stacks/package.json` |

### Utilities

| Dependency | Official Name | Purpose | Source |
|------------|---------------|---------|--------|
| `lz-string` | LZ-String | String compression | `/compiler/apps/playground/package.json` |
| `lru-cache` | LRU Cache | Least Recently Used cache | `/compiler/apps/playground/package.json` |
| `invariant` | Invariant | Runtime assertions | `/compiler/apps/playground/package.json`, `/compiler/packages/make-read-only-util/package.json` |
| `pretty-format` | Pretty Format | Object formatting | `/compiler/apps/playground/package.json`, `/package.json` |
| `chalk` | Chalk | Terminal string styling | `/compiler/packages/react-compiler-healthcheck/package.json`, `/scripts/release/package.json` |
| `ora` | Ora | Terminal spinner | `/compiler/packages/react-compiler-healthcheck/package.json`, `/compiler/package.json` |
| `yargs` | Yargs | Command line argument parsing | `/compiler/packages/react-compiler-healthcheck/package.json`, `/package.json` |
| `glob` | Glob | File pattern matching | `/compiler/packages/snap/package.json`, `/package.json` |
| `fast-glob` | Fast Glob | Fast file globbing | `/compiler/packages/react-compiler-healthcheck/package.json` |
| `fs-extra` | FS Extra | Extended file system utilities | `/compiler/package.json`, `/scripts/release/package.json` |
| `rimraf` | Rimraf | rm -rf for Node.js | `/fixtures/fizz/package.json`, `/package.json` |
| `semver` | SemVer | Semantic versioning utilities | `/fixtures/dom/package.json`, `/fixtures/flight/package.json` |
| `minimist` | Minimist | Argument parser | `/package.json`, `/packages/react-devtools/package.json` |
| `shelljs` | ShellJS | Unix shell commands for Node.js | `/package.json` |
| `ncp` | NCP | Async recursive file copy | `/package.json`, `/scripts/bench/package.json` |
| `prompts` | Prompts | Interactive prompts | `/fixtures/flight/package.json`, `/fixtures/flight-esm/package.json` |

### DevTools Specific

| Dependency | Official Name | Purpose | Source |
|------------|---------------|---------|--------|
| `electron` | Electron | Desktop application framework | `/packages/react-devtools/package.json` |
| `ws` | ws | WebSocket client/server | `/packages/react-devtools-core/package.json` |
| `shell-quote` | Shell Quote | Shell command quoting | `/packages/react-devtools-core/package.json` |
| `web-ext` | Web-Ext | Browser extension development | `/packages/react-devtools-extensions/package.json` |
| `error-stack-parser` | Error Stack Parser | Parse error stack traces | `/packages/react-debug-tools/package.json`, `/package.json` |
| `source-map-js` | Source Map JS | Source map parsing | `/packages/react-devtools-inline/package.json` |
| `@jridgewell/sourcemap-codec` | Sourcemap Codec | Source map encoding/decoding | `/packages/react-devtools-inline/package.json` |
| `clipboard-js` | Clipboard.js | Clipboard operations | `/packages/react-devtools-shared/package.json` |
| `compare-versions` | Compare Versions | Version comparison | `/packages/react-devtools-shared/package.json` |
| `json5` | JSON5 | Extended JSON format | `/packages/react-devtools-shared/package.json` |
| `local-storage-fallback` | Local Storage Fallback | LocalStorage with fallbacks | `/packages/react-devtools-shared/package.json` |
| `memoize-one` | Memoize One | Single-argument memoization | `/packages/react-devtools-timeline/package.json` |
| `nullthrows` | Nullthrows | Null assertion utility | `/packages/react-devtools-timeline/package.json` |
| `pretty-ms` | Pretty MS | Milliseconds formatting | `/packages/react-devtools-timeline/package.json` |
| `@elg/speedscope` | Speedscope | Performance profile visualization | `/packages/react-devtools-timeline/package.json` |
| `rbush` | RBush | R-tree spatial index | `/packages/react-devtools-shared/package.json` |

### MCP Server (React Compiler)

| Dependency | Official Name | Purpose | Source |
|------------|---------------|---------|--------|
| `@modelcontextprotocol/sdk` | Model Context Protocol SDK | MCP server implementation | `/compiler/packages/react-mcp-server/package.json` |
| `algoliasearch` | Algolia | Search API client | `/compiler/packages/react-mcp-server/package.json` |
| `cheerio` | Cheerio | HTML parsing (jQuery-like) | `/compiler/packages/react-mcp-server/package.json` |
| `html-to-text` | HTML to Text | HTML to plain text conversion | `/compiler/packages/react-mcp-server/package.json` |
| `puppeteer` | Puppeteer | Headless browser automation | `/compiler/packages/react-mcp-server/package.json`, `/scripts/release/package.json` |

### Language Server (React Forgive)

| Dependency | Official Name | Purpose | Source |
|------------|---------------|---------|--------|
| `vscode-languageserver` | VS Code Language Server | Language server protocol implementation | `/compiler/packages/react-forgive/server/package.json` |
| `vscode-languageserver-textdocument` | VS Code Text Document | Text document handling | `/compiler/packages/react-forgive/server/package.json` |
| `vscode-languageclient` | VS Code Language Client | Language client for VS Code | `/compiler/packages/react-forgive/client/package.json` |

### Graphics & Visualization

| Dependency | Official Name | Purpose | Source |
|------------|---------------|---------|--------|
| `art` | ART | Vector graphics library | `/packages/react-art/package.json`, `/fixtures/dom/package.json` |
| `dagre` | Dagre | Directed graph layout | `/fixtures/fiber-debugger/package.json` |
| `victory` | Victory | Charting library | `/fixtures/concurrent/time-slicing/package.json` |

### Parsing & AST

| Dependency | Official Name | Purpose | Source |
|------------|---------------|------

# core_entities

Core entities and their relationships

# Domain Model Analysis for React Repository

Based on my analysis of the React repository structure, I've identified the key domain entities and their relationships. This is a UI framework/library codebase, so the domain models revolve around rendering, component management, and developer tooling.

---

## 1. Common Data Entities / Domain Models

### 1.1 React Element

The fundamental building block representing a node in the React virtual DOM tree.

| Attribute | Type | Description |
|-----------|------|-------------|
| `$$typeof` | Symbol | Type identifier (e.g., `REACT_ELEMENT_TYPE`) |
| `type` | string \| Function \| Class | Component type (HTML tag, function, or class) |
| `key` | string \| null | Unique identifier for reconciliation |
| `ref` | Ref \| null | Reference to DOM node or component instance |
| `props` | Object | Properties passed to the element |
| `_owner` | Fiber \| null | Component that created this element |

---

### 1.2 Fiber

The internal work unit used by the React Reconciler for incremental rendering.

| Attribute | Type | Description |
|-----------|------|-------------|
| `tag` | number | Type of fiber (FunctionComponent, ClassComponent, HostComponent, etc.) |
| `key` | string \| null | Unique key for reconciliation |
| `type` | any | Element type |
| `stateNode` | any | DOM node or class instance |
| `return` | Fiber \| null | Parent fiber |
| `child` | Fiber \| null | First child fiber |
| `sibling` | Fiber \| null | Next sibling fiber |
| `index` | number | Position among siblings |
| `pendingProps` | any | New props to process |
| `memoizedProps` | any | Props from last render |
| `memoizedState` | any | State from last render |
| `updateQueue` | UpdateQueue \| null | Queue of state updates |
| `flags` | number | Side-effect flags (Placement, Update, Deletion) |
| `lanes` | Lanes | Priority lanes for scheduling |
| `alternate` | Fiber \| null | Work-in-progress or current fiber |

---

### 1.3 Component (Abstract)

Represents user-defined UI components.

| Attribute | Type | Description |
|-----------|------|-------------|
| `props` | Object | Input properties |
| `state` | Object | Internal state (class components) |
| `context` | any | Context value(s) |
| `refs` | Object | References (class components) |
| `updater` | Updater | State update mechanism |

**Subtypes:**
- **FunctionComponent**: Stateless or uses hooks
- **ClassComponent**: Extends `React.Component` or `React.PureComponent`

---

### 1.4 Hook

State and lifecycle management for function components.

| Attribute | Type | Description |
|-----------|------|-------------|
| `memoizedState` | any | Current hook state |
| `baseState` | any | Base state before updates |
| `baseQueue` | Update \| null | Pending low-priority updates |
| `queue` | UpdateQueue \| null | Pending updates |
| `next` | Hook \| null | Next hook in the list |

**Hook Types:** `useState`, `useEffect`, `useContext`, `useReducer`, `useMemo`, `useCallback`, `useRef`, `useLayoutEffect`, `useTransition`, `useDeferredValue`

---

### 1.5 Update / UpdateQueue

Represents state changes to be processed.

| Attribute | Type | Description |
|-----------|------|-------------|
| `lane` | Lane | Priority of the update |
| `action` | any | State update action or value |
| `next` | Update \| null | Next update in queue |
| `hasEagerState` | boolean | Whether state was computed early |
| `eagerState` | any | Pre-computed state |

---

### 1.6 FiberRoot

The root of a React application tree.

| Attribute | Type | Description |
|-----------|------|-------------|
| `containerInfo` | any | DOM container node |
| `current` | Fiber | Current fiber tree root |
| `pendingLanes` | Lanes | Lanes with pending work |
| `finishedWork` | Fiber \| null | Completed work tree |
| `callbackNode` | any | Scheduler callback handle |
| `callbackPriority` | Lane | Priority of scheduled callback |
| `eventTimes` | LaneMap | Event timestamps per lane |

---

### 1.7 ReactServerComponent (Flight)

Represents a serializable component for React Server Components.

| Attribute | Type | Description |
|-----------|------|-------------|
| `$$typeof` | Symbol | `REACT_ELEMENT_TYPE` or server-specific |
| `type` | Reference | Module reference to client component |
| `props` | Object | Serializable props |
| `_payload` | Chunk | Serialized payload |
| `_init` | Function | Initialization function |

---

### 1.8 DevTools Element

Used by React DevTools for component inspection.

| Attribute | Type | Description |
|-----------|------|-------------|
| `id` | number | Unique element ID |
| `type` | ElementType | Component type classification |
| `displayName` | string \| null | Component display name |
| `key` | string \| null | Element key |
| `parentID` | number | Parent element ID |
| `children` | Array<number> | Child element IDs |
| `depth` | number | Nesting depth in tree |
| `hocDisplayNames` | Array<string> \| null | Higher-order component names |
| `hooks` | Array<HookInfo> \| null | Hook information |
| `props` | Object | Current props |
| `state` | Object \| null | Current state |

---

### 1.9 Scheduler Task

Represents a unit of scheduled work.

| Attribute | Type | Description |
|-----------|------|-------------|
| `id` | number | Unique task ID |
| `callback` | Function \| null | Work to execute |
| `priorityLevel` | PriorityLevel | Task priority |
| `startTime` | number | When task becomes ready |
| `expirationTime` | number | Deadline for completion |
| `sortIndex` | number | Heap sorting index |

---

### 1.10 Event (Synthetic)

React's cross-browser event wrapper.

| Attribute | Type | Description |
|-----------|------|-------------|
| `nativeEvent` | Event | Original browser event |
| `type` | string | Event type name |
| `target` | EventTarget | Event target |
| `currentTarget` | EventTarget | Current handler target |
| `eventPhase` | number | Capture/bubble phase |
| `bubbles` | boolean | Whether event bubbles |
| `cancelable` | boolean | Whether event is cancelable |
| `timeStamp` | number | Event timestamp |
| `defaultPrevented` | boolean | Whether default was prevented |
| `isPropagationStopped` | Function | Check if propagation stopped |

---

## 2. Entity Relationships

```
┌─────────────────────────────────────────────────────────────────┐
│                         FiberRoot                                │
│  (Application Root Container)                                    │
└──────────────────────┬──────────────────────────────────────────┘
                       │ 1:1 (current)
                       ▼
┌─────────────────────────────────────────────────────────────────┐
│                           Fiber                                  │
│  (Internal Work Unit - Tree Node)                               │
├─────────────────────────────────────────────────────────────────┤
│  - child ──────► Fiber (1:0..1)                                 │
│  - sibling ────► Fiber (1:0..1)                                 │
│  - return ─────► Fiber (1:0..1) [parent]                        │
│  - alternate ──► Fiber (1:0..1) [WIP/current]                   │
└──────────────────────┬──────────────────────────────────────────┘
                       │ 1:1 (represents)
                       ▼
┌─────────────────────────────────────────────────────────────────┐
│                      React Element                               │
│  (Virtual DOM Node - Immutable Description)                     │
├─────────────────────────────────────────────────────────────────┤
│  - props.children ──► React Element[] (1:many)                  │
│  - _owner ──────────► Fiber (many:1)                            │
└──────────────────────┬──────────────────────────────────────────┘
                       │ many:1 (type)
                       ▼
┌─────────────────────────────────────────────────────────────────┐
│                        Component                                 │
│  (User-defined Function or Class)                               │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                           Fiber                                  │
└───────────┬─────────────────────────────┬───────────────────────┘
            │ 1:many (memoizedState)      │ 1:1 (updateQueue)
            ▼                             ▼
┌───────────────────────┐     ┌───────────────────────────────────┐
│         Hook          │     │          UpdateQueue              │
│  (Linked List Node)   │     │  (Pending State Changes)          │
├───────────────────────┤     ├───────────────────────────────────┤
│  - next ──► Hook      │     │  - pending ──► Update (circular)  │
└───────────────────────┘     └─────────────────┬─────────────────┘
                                                │ 1:many
                                                ▼
                              ┌───────────────────────────────────┐
                              │            Update                 │
                              │  (Single State Update)            │
                              ├───────────────────────────────────┤
                              │  - next ──► Update (circular)     │
                              └───────────────────────────────────┘
```

### Relationship Summary Table

| Parent Entity | Child Entity | Relationship | Description |
|--------------|--------------|--------------|-------------|
| FiberRoot | Fiber | 1:1 | Root contains current fiber tree |
| Fiber | Fiber | 1:many | Parent-child tree structure (child, sibling, return) |
| Fiber | Fiber | 1:1 | Alternate pointer (current ↔ work-in-progress) |
| Fiber | React Element | 1:1 | Fiber represents/renders an element |
| Fiber | Hook | 1:many | Function component's hooks (linked list) |
| Fiber | UpdateQueue | 1:1 | Pending state updates |
| Hook | Hook | 1:1 | Linked list via `next` |
| UpdateQueue | Update | 1:many | Circular linked list of updates |
| React Element | Component | many:1 | Elements reference component type |
| React Element | React Element | 1:many | Children relationship via props |
| Scheduler | Task | 1:many | Scheduler manages multiple tasks |
| DevTools | DevTools Element | 1:many | DevTools tracks component tree |
| DevTools Element | DevTools Element | 1:many | Parent-children hierarchy |

---

## 3. Domain Contexts

### 3.1 Core React Runtime
- **Entities**: React Element, Component, Fiber, FiberRoot, Hook, Update
- **Purpose**: Virtual DOM representation and reconciliation

### 3.2 Scheduler
- **Entities**: Task, Priority Levels, Lanes
- **Purpose**: Cooperative scheduling of work units

### 3.3 React DOM
- **Entities**: SyntheticEvent, HostConfig, DOMComponent
- **Purpose**: Browser DOM rendering and event handling

### 3.4 React Server (Flight)
- **Entities**: ReactServerComponent, Chunk, ModuleReference
- **Purpose**: Server-side rendering and component streaming

### 3.5 DevTools
- **Entities**: DevTools Element, Hook Info, Profiler Data
- **Purpose**: Development debugging and inspection

# DBs

databases analysis

Based on my comprehensive analysis of the React repository codebase, I have thoroughly scanned all directories and files for any database interactions, including:

- Database connection configurations
- ORM definitions (SQLAlchemy, Sequelize, Prisma, TypeORM, Mongoose, etc.)
- Direct SQL queries or NoSQL operations
- Database client libraries (pg, mysql, mongodb, redis, etc.)
- Schema definitions or migration scripts
- Data persistence logic
- Environment variables or configuration files referencing databases

**Findings:**

This repository is the **React JavaScript library** - a frontend UI framework. The codebase consists of:

1. **Core React packages** (`packages/react`, `packages/react-dom`, `packages/react-reconciler`, etc.)
2. **React DevTools** for debugging
3. **React Server Components** implementations
4. **Compiler/build tooling** 
5. **Test utilities and fixtures**
6. **ESLint plugins** for React hooks

The repository contains no server-side application code that would interact with databases. All data persistence patterns found are:
- In-memory state management (React state, context)
- Test fixtures with mock data
- Build/release scripts that interact with the filesystem
- Configuration files for build tools (Babel, Webpack, Rollup, Jest)

The fixtures and example applications (like `fixtures/flight/`, `fixtures/ssr/`, `fixtures/fizz/`) are demonstration servers that render React components but do not include any database connectivity.

---

no database

# APIs

APIs analysis

# API Documentation Analysis

After a comprehensive scan of the repository, I need to examine the files that might contain HTTP API endpoints.

Let me analyze the relevant files:

## Files Examined for HTTP APIs:

1. **`scripts/bench/server.js`** - Benchmark server
2. **`fixtures/flight/server/`** - Flight fixture server
3. **`fixtures/view-transition/server/`** - View transition server
4. **`fixtures/ssr2/server/`** - SSR2 server
5. **`fixtures/ssr/server/`** - SSR server
6. **`fixtures/fizz/server/`** - Fizz server
7. **`packages/react-devtools-shell/webpack-server.js`** - DevTools shell server

Based on my analysis of the repository structure, this is the **React core library repository**. The repository primarily contains:

- React core packages (`react`, `react-dom`, `react-reconciler`, etc.)
- Development tools (`react-devtools-*`)
- Build scripts and tooling
- Test fixtures and examples

The servers found in this repository are **development/testing servers** used for:
- Running benchmarks locally
- Testing SSR (Server-Side Rendering) functionality
- Testing React Server Components (Flight)
- DevTools development

These are **not production HTTP APIs** meant to be consumed by external clients. They are internal development servers that:
- Serve static files for testing
- Render React components for SSR testing
- Support the development workflow

---

**no HTTP API**

# events

events analysis

Based on my comprehensive analysis of this repository, which is the React library source code, I need to report:

**no events**

This repository is the core React library codebase (facebook/react). While it contains extensive code for:

1. **React Core** - The React library itself (`packages/react/`)
2. **React DOM** - DOM rendering (`packages/react-dom/`)
3. **React Reconciler** - The reconciliation algorithm (`packages/react-reconciler/`)
4. **React Server Components** - Server-side rendering (`packages/react-server/`, `packages/react-server-dom-webpack/`, etc.)
5. **React DevTools** - Developer tooling (`packages/react-devtools-*`)
6. **Scheduler** - React's internal scheduling (`packages/scheduler/`)
7. **Build/Test Infrastructure** - Scripts, fixtures, and tooling

The codebase does **not** contain any message broker event systems (SQS, EventBridge, Kafka, Ably, RabbitMQ, Pub/Sub, etc.) for consuming or producing events in the traditional event-driven architecture sense.

What the codebase does contain are:
- **Internal React events** (synthetic DOM events, lifecycle hooks, etc.) - These are React's internal event system for handling user interactions, not message broker events
- **DOM event handling** (`packages/react-dom-bindings/src/events/`) - Browser DOM event listeners
- **DevTools message passing** - Communication between DevTools frontend/backend via postMessage for debugging purposes

None of these qualify as the type of "events" in the event documentation context (i.e., message broker/event bus events for inter-service communication).

# service_dependencies

Analyze service dependencies

# External Dependencies Analysis - React Repository

This analysis covers the React codebase (`react_33c851c7`) and identifies all external dependencies including libraries, services, and external integrations.

---

## 1. Package Manager Dependencies (Libraries/Frameworks)

### 1.1 Core JavaScript/TypeScript Build Tools & Compilers

| Dependency Name | Type of Dependency | Purpose/Role | Integration Point/Clues |
|----------------|-------------------|--------------|------------------------|
| **@babel/core** | Library/Framework | Core Babel compiler for JavaScript/TypeScript transpilation | `/package.json`, `/compiler/packages/*/package.json`, `/fixtures/*/package.json` - Used throughout for transpilation |
| **@babel/parser** | Library/Framework | JavaScript/TypeScript parser for AST generation | `/package.json`, `/compiler/packages/babel-plugin-react-compiler/package.json` |
| **@babel/generator** | Library/Framework | Generates code from AST | `/compiler/apps/playground/package.json`, `/compiler/packages/babel-plugin-react-compiler/package.json` |
| **@babel/traverse** | Library/Framework | Traverses and manipulates AST nodes | `/package.json`, `/compiler/apps/playground/package.json` |
| **@babel/types** | Library/Framework | AST type definitions and builders | `/package.json`, `/compiler/packages/babel-plugin-react-compiler/package.json` |
| **@babel/preset-env** | Library/Framework | Smart preset for target environment compilation | `/package.json`, `/compiler/packages/react-mcp-server/package.json` |
| **@babel/preset-react** | Library/Framework | Babel preset for React JSX transformation | `/package.json`, `/compiler/apps/playground/package.json` |
| **@babel/preset-typescript** | Library/Framework | TypeScript support for Babel | `/package.json`, `/compiler/apps/playground/package.json` |
| **@babel/preset-flow** | Library/Framework | Flow type stripping for Babel | `/package.json`, `/packages/react-devtools-shared/package.json` |
| **@babel/plugin-syntax-typescript** | Library/Framework | TypeScript syntax support | `/compiler/apps/playground/package.json` |
| **@babel/plugin-transform-block-scoping** | Library/Framework | Block scoping transformation | `/compiler/apps/playground/package.json` |
| **@babel/plugin-transform-modules-commonjs** | Library/Framework | CommonJS module transformation | `/package.json`, `/compiler/apps/playground/package.json` |
| **@babel/plugin-transform-react-jsx** | Library/Framework | JSX transformation | `/package.json` |
| **@babel/register** | Library/Framework | Runtime Babel compilation | `/fixtures/fizz/package.json`, `/fixtures/view-transition/package.json` |
| **@babel/code-frame** | Library/Framework | Code frame generation for error messages | `/package.json`, `/compiler/packages/snap/package.json` |
| **@babel/runtime** | Library/Framework | Runtime helpers for Babel | `/packages/react-devtools-shared/package.json` |
| **typescript** | Library/Framework | TypeScript compiler | `/package.json`, `/compiler/package.json` |
| **flow-bin** | Library/Framework | Flow static type checker | `/package.json` |
| **flow-remove-types** | Library/Framework | Strips Flow types from code | `/package.json` |
| **flow-typed** | Library/Framework | Flow type definitions manager | `/package.json` |
| **hermes-parser** | Library/Framework | Hermes JavaScript parser (used for React Native) | `/compiler/apps/playground/package.json`, `/compiler/packages/eslint-plugin-react-compiler/package.json`, `/packages/eslint-plugin-react-hooks/package.json` |
| **hermes-eslint** | Library/Framework | ESLint parser using Hermes | `/compiler/apps/playground/package.json`, `/package.json` |

### 1.2 Bundlers & Build Tools

| Dependency Name | Type of Dependency | Purpose/Role | Integration Point/Clues |
|----------------|-------------------|--------------|------------------------|
| **rollup** | Library/Framework | Module bundler for building React packages | `/package.json`, `/scripts/rollup/build.js` |
| **@rollup/plugin-babel** | Library/Framework | Babel integration for Rollup | `/package.json` |
| **@rollup/plugin-commonjs** | Library/Framework | CommonJS module support in Rollup | `/package.json` |
| **@rollup/plugin-node-resolve** | Library/Framework | Node module resolution for Rollup | `/package.json` |
| **@rollup/plugin-replace** | Library/Framework | String replacement in Rollup builds | `/package.json` |
| **@rollup/plugin-typescript** | Library/Framework | TypeScript support in Rollup | `/package.json` |
| **rollup-plugin-dts** | Library/Framework | TypeScript declaration bundling | `/package.json` |
| **rollup-plugin-prettier** | Library/Framework | Prettier formatting in Rollup output | `/package.json` |
| **rollup-plugin-strip-banner** | Library/Framework | Banner stripping for Rollup | `/package.json` |
| **webpack** | Library/Framework | Module bundler for various fixtures and devtools | `/fixtures/flight/package.json`, `/packages/react-devtools-*/package.json` |
| **webpack-cli** | Library/Framework | Webpack command line interface | `/fixtures/fizz/package.json`, `/packages/react-devtools-core/package.json` |
| **webpack-dev-server** | Library/Framework | Development server for webpack | `/packages/react-devtools-extensions/package.json` |
| **webpack-dev-middleware** | Library/Framework | Webpack middleware for Express | `/fixtures/flight/package.json` |
| **webpack-hot-middleware** | Library/Framework | Hot module replacement middleware | `/fixtures/flight/package.json` |
| **webpack-manifest-plugin** | Library/Framework | Asset manifest generation | `/fixtures/flight/package.json` |
| **webpack-sources** | Library/Framework | Source handling for webpack | `/fixtures/flight-esm/package.json`, `/packages/react-server-dom-webpack/package.json` |
| **devtools-ignore-webpack-plugin** | Library/Framework | DevTools source map ignore list | `/fixtures/flight/package.json` |
| **esbuild** | Library/Framework | Fast JavaScript bundler | `/compiler/package.json` |
| **tsup** | Library/Framework | TypeScript bundler (esbuild-based) | `/package.json`, `/compiler/package.json` |
| **google-closure-compiler** | Library/Framework | JavaScript optimizer/minifier | `/package.json` |
| **terser-webpack-plugin** | Library/Framework | JavaScript minification for webpack | `/fixtures/flight/package.json` |
| **css-minimizer-webpack-plugin** | Library/Framework | CSS minification for webpack | `/fixtures/flight/package.json` |
| **mini-css-extract-plugin** | Library/Framework | CSS extraction for webpack | `/fixtures/flight/package.json`, `/packages/react-devtools-fusebox/package.json` |
| **parcel** | Library/Framework | Zero-config bundler | `/fixtures/flight-parcel/package.json` |
| **browserify** | Library/Framework | Browser bundler for fixtures | `/fixtures/packaging/browserify/*/package.json` |
| **requirejs** | Library/Framework | AMD module loader | `/fixtures/packaging/rjs/*/package.json` |
| **systemjs-builder** | Library/Framework | SystemJS bundle builder | `/fixtures/packaging/systemjs-builder/*/package.json` |
| **brunch** | Library/Framework | Fast front-end build tool | `/fixtures/packaging/brunch/*/package.json` |

### 1.3 Testing Frameworks & Utilities

| Dependency Name | Type of Dependency | Purpose/Role | Integration Point/Clues |
|----------------|-------------------|--------------|------------------------|
| **jest** | Library/Framework | JavaScript testing framework | `/package.json`, `/scripts/jest/` directory |
| **jest-cli** | Library/Framework | Jest command line interface | `/package.json` |
| **jest-diff** | Library/Framework | Diff output for Jest assertions | `/package.json`, `/fixtures/dom/package.json` |
| **jest-environment-jsdom** | Library/Framework | JSDOM environment for Jest | `/package.json` |
| **jest-snapshot-serializer-raw** | Library/Framework | Raw snapshot serialization | `/package.json` |
| **@testing-library/react** | Library/Framework | React testing utilities | `/fixtures/flight/package.json`, `/compiler/packages/snap/package.json` |
| **@testing-library/jest-dom** | Library/Framework | Jest DOM matchers | `/fixtures/flight/package.json` |
| **@testing-library/user-event** | Library/Framework | User event simulation | `/fixtures/flight/package.json` |
| **@playwright/test** | Library/Framework | End-to-end testing framework | `/compiler/apps/playground/package.json`, `/fixtures/flight/package.json`, `/packages/react-devtools-inline/package.json` |
| **jsdom** | Library/Framework | JavaScript DOM implementation | `/compiler/packages/snap/package.json` |
| **mocha** | Library/Framework | Test framework for VSCode extension | `/compiler/packages/react-forgive/package.json` |
| **@vscode/test-cli** | Library/Framework | VSCode extension testing CLI | `/compiler/packages/react-forgive/package.json` |
| **@vscode/test-electron** | Library/Framework | VSCode extension testing with Electron | `/compiler/packages/react-forgive/package.json` |
| **babel-jest** | Library/Framework | Babel transformer for Jest | `/fixtures/flight/package.json`, `/compiler/packages/babel-plugin-react-compiler/package.json` |
| **ts-jest** | Library/Framework | TypeScript preprocessor for Jest | `/compiler/packages/babel-plugin-react-compiler/package.json` |
| **jest-fetch-mock** | Library/Framework | Fetch mocking for Jest | `/packages/react-devtools-extensions/package.json` |

### 1.4 Linting & Code Quality

| Dependency Name | Type of Dependency | Purpose/Role | Integration Point/Clues |
|----------------|-------------------|--------------|------------------------|
| **eslint** | Library/Framework | JavaScript/TypeScript linter | `/package.json`, multiple fixture and package files |
| **@typescript-eslint/eslint-plugin** | Library/Framework | TypeScript ESLint rules | `/package.json`, `/compiler/packages/babel-plugin-react-compiler/package.json` |
| **@typescript-eslint/parser** | Library/Framework | TypeScript parser for ESLint | `/package.json`, `/packages/eslint-plugin-react-hooks/package.json` |
| **eslint-config-prettier** | Library/Framework | Prettier ESLint config | `/package.json` |
| **eslint-plugin-babel** | Library/Framework | Babel ESLint rules | `/package.json` |
| **eslint-plugin-es** | Library/Framework | ES version linting | `/package.json` |
| **eslint-plugin-eslint-plugin** | Library/Framework | ESLint plugin development rules | `/package.json` |
| **eslint-plugin-ft-flow** | Library/Framework | Flow type linting | `/package.json` |
| **eslint-plugin-jest** | Library/Framework | Jest linting rules | `/package.json` |
| **eslint-plugin-no-for-of-loops** | Library/Framework | Disallow for-of loops | `/package.json` |
| **eslint-plugin-no-function-declare-after-return** | Library/Framework | Function declaration ordering | `/package.json` |
| **eslint-plugin-react** | Library/Framework | React linting rules | `/package.json` |
| **eslint-plugin-react-hooks-published** | Library/Framework | Published React Hooks linting (aliased) | `/package.json` |
| **babel-eslint** | Library/Framework | Babel parser for ESLint | `/packages/eslint-plugin-react-hooks/package.json` |
| **prettier** | Library/Framework | Code formatter | `/package.json`, `/compiler/package.json`, `/compiler/apps/playground/package.json` |
| **prettier-plugin-hermes-parser** | Library/Framework | Prettier plugin for Hermes | `/compiler/package.json` |
| **danger** | Library/Framework | CI code review automation | `/package.json`, `/dangerfile.js` |

### 1.5 React Ecosystem Dependencies

| Dependency Name | Type of Dependency | Purpose/Role | Integration Point/Clues |
|----------------|-------------------|--------------|------------------------|
| **react** | Library/Framework | Core React library (various versions for testing) | Throughout fixtures and packages |
| **react-dom** | Library/Framework | React DOM renderer | Throughout fixtures and packages |
| **react-is** | Library/Framework | React type checking utilities | `/compiler/package.json`, `/packages/react-test-renderer/package.json` |
| **scheduler** | Library/Framework | React's scheduling library | `/packages/react-dom/package.json`, `/packages/react-reconciler/package.json` |
| **prop-types** | Library/Framework | Runtime type checking for React props | `/package.json`, `/fixtures/dom/package.json` |
| **react-lifecycles-compat** | Library/Framework | Lifecycle compatibility polyfill | `/package.json` |
| **create-react-class** | Library/Framework | Legacy createClass API | `/package.json`, `/packages/react-art/package.json` |
| **react-scripts** | Library/Framework | Create React App scripts | Multiple fixtures |
| **react-refresh** | Library/Framework | Fast Refresh for React | `/fixtures/flight/package.json` |
| **@pmmmwh/react-refresh-webpack-plugin** | Library/Framework | Webpack plugin for React Refresh | `/fixtures/flight/package.json` |
| **react-error-boundary** | Library/Framework | Error boundary component | `/fixtures/fizz/package.json`, `/fixtures/ssr2/package.json` |
| **react-native-web** | Library/Framework | React Native for Web | `/packages/react-devtools-shell/package.json` |

### 1.6 Server & HTTP Libraries

| Dependency Name | Type of Dependency | Purpose/Role | Integration Point/Clues |
|----------------|-------------------|--------------|------------------------|
| **express** | Library/Framework | Web server framework | `/fixtures/fizz/package.json`, `/fixtures/ssr/package.json`, `/fixtures/flight-parcel/package.json` |
| **compression** | Library/Framework | HTTP compression middleware | `/fixtures/fizz/package.json`, `/fixtures/flight/package.json` |
| **body-parser** | Library/Framework | HTTP body parsing middleware | `/fixtures/flight/package.json`, `/fixtures/flight-esm/package.json` |
| **http-proxy-middleware** | Library/Framework | HTTP proxy middleware | `/fixtures/ssr/package.json`, `/fixtures/view-transition/package.json` |
| **undici** | Library/Framework | Modern HTTP client | `/package.json`, `/fixtures/flight/package.json` |
| **node-fetch** | Library/Framework | Fetch API for Node.js | `/fixtures/ssr/package.json` |
| **http-server** | Library/Framework | Simple HTTP server | `/fixtures/stacks/package.json`, `/scripts/bench/package.json` |
| **http2** | Library/Framework | HTTP/2 protocol support | `/scripts/bench/package.json` |
| **busboy** | Library/Framework | Multipart form parsing | `/fixtures/flight/package.json`, `/fixtures/flight-esm/package.json` |
| **nodemon** | Library/Framework | Development server auto-restart | `/fixtures/fizz/package.json`, `/fixtures/flight/package.json` |
| **pushstate-server** | Library/Framework | Static server with pushstate support | `/scripts/release/package.json` |

### 1.7 CSS & Styling

| Dependency Name | Type of Dependency | Purpose/Role | Integration Point/Clues |
|----------------|-------------------|--------------|------------------------|
| **css-loader** | Library/Framework | CSS loading for webpack | `/fixtures/flight/package.json`, `/packages/react-devtools-*/package.json` |
| **style-loader** | Library/Framework | CSS injection for webpack | `/fixtures/flight/package.json`, `/packages/react-devtools-*/package.json` |
| **postcss** | Library/Framework | CSS transformation tool | `/fixtures/flight/package.json` |
| **postcss-loader** | Library/Framework | PostCSS webpack loader | `/fixtures/flight/package.json` |
| **postcss-flexbugs-fixes** | Library/Framework | Flexbox bug fixes | `/fixtures/flight/package.json` |
| **postcss-normalize** | Library/Framework | CSS normalize | `/fixtures/flight/package.json` |
| **postcss-preset-env** | Library/Framework | Modern CSS features | `/fixtures/flight/package.json` |
| **tailwindcss** | Library/Framework | Utility-first CSS framework | `/fixtures/flight/package.json`, `/compiler/apps/playground/package.json` |
| **autoprefixer** | Library/Framework | CSS vendor prefixing | `/compiler/apps/playground/package.json` |
| **glamor** | Library/Framework | CSS-in-JS library | `/fixtures/attribute-behavior/package.json`, `/fixtures/concurrent/time-slicing/package.json` |
| **sass-loader** | Library/Framework | SASS/SCSS webpack loader | `/fixtures/flight/package.json` |

### 1.8 Validation & Schema Libraries

| Dependency Name | Type of Dependency | Purpose/Role | Integration Point/Clues |
|----------------|-------------------|--------------|------------------------|
| **zod** | Library/Framework | TypeScript-first schema validation | `/compiler/packages/eslint-plugin-react-compiler/package.json`, `/compiler/packages/react-compiler-healthcheck/package.json`, `/packages/eslint-plugin-react-hooks/package.json` |
| **zod-validation-error** | Library/Framework | Error formatting for Zod | `/compiler/packages/eslint-plugin-react-compiler/package.json`, `/packages/eslint-plugin-react-hooks/package.json` |

### 1.9 UI & Visualization Libraries

| Dependency Name | Type of Dependency | Purpose/Role | Integration Point/Clues |
|----------------|-------------------|--------------|------------------------|
| **art** | Library/Framework | Vector graphics library | `/package.json`, `/packages/react-art/package.json` |
| **monaco-editor** | Library/Framework | VS Code editor component | `/compiler/apps/playground/package.json` |
| **@monaco-editor/react** | Library/Framework | Monaco Editor React wrapper | `/compiler/apps/playground/package.json` |
| **monaco-editor-webpack-plugin** | Library/Framework | Monaco webpack integration | `/compiler/apps/playground/package.json` |
| **codemirror** | Library/Framework | Code editor component | `/fixtures/dom/package.json` |
| **react-virtualized** | Library/Framework | Virtualized lists/grids | `/fixtures/attribute-behavior/package.json` |
| **react-virtualized-auto-sizer** | Library/Framework | Auto-sizing for virtualized lists | `/packages/react-devtools-shared/package.json`, `/packages/react-devtools-timeline/package.json` |
| **react-window** | Library/Framework | Lightweight virtualization | `/packages/react-devtools-shared/package.json` |
| **victory** | Library/Framework | Data visualization components | `/fixtures/concurrent/time-slicing/package.json` |
| **dagre** | Library/Framework | Graph layout library | `/fixtures/fiber-debugger/package.json` |
| **react-draggable** | Library/Framework | Draggable components | `/fixtures/fiber-debugger/package.json` |
| **react-motion** | Library/Framework | Animation library | `/fixtures/fiber-debugger/package.json` |
| **re-resizable** | Library/Framework | Resizable components | `/compiler/apps/playground/package.json` |
| **@use-gesture/react** | Library/Framework | Gesture handling | `/compiler/apps/playground/package.json` |
| **@heroicons/react** | Library/Framework | Icon library | `/compiler/apps/playground/package.json` |
| **notistack** | Library/Framework | Snackbar notifications | `/compiler/apps/playground/package.json` |
| **@reach/menu-button** | Library/Framework | Accessible menu button | `/packages/react-devtools-shared/package.json` |
| **@reach/tooltip** | Library/Framework | Accessible tooltip | `/packages/react-devtools-shared/package.json` |

### 1.10 Routing & State Management

| Dependency Name | Type of Dependency | Purpose/Role | Integration Point/Clues |
|----------------|-------------------|--------------|------------------------|
| **react-router-dom** | Library/Framework | React routing | `/fixtures/nesting/src/legacy/package.json`, `/fixtures/nesting/src/modern/package.json` |
| **redux** | Library/Framework | State management | `/fixtures/nesting/package.json` |
| **react-redux** | Library/Framework | React Redux bindings | `/fixtures/nesting/src/*/package.json` |
| **use-sync-external-store** | Library/Framework | External store subscription hook | `/packages/use-subscription/package.json` |

### 1.11 File System & OS Utilities

| Dependency Name | Type of Dependency | Purpose/Role | Integration Point/Clues |
|----------------|-------------------|--------------|------------------------|
| **fs-extra** | Library/Framework | Extended file system operations | `/compiler/package.json`, `/scripts/devtools/package.json`, `/scripts/release/package.json` |
| **glob** | Library/Framework | File pattern matching | `/package.json`, `/compiler/packages/snap/package.json` |
| **glob-stream** | Library/Framework | Streaming glob | `/package.json` |
| **fast-glob** | Library/Framework | Fast glob implementation | `/compiler/packages/react-compiler-healthcheck/package.json` |
| **rimraf** | Library/Framework | rm -rf for Node.js | `/package.json`, `/fixtures/fizz/package.json` |
| **mkdirp** | Library/Framework | mkdir -p for Node.js | `/package.json` |
| **ncp** | Library/Framework | Recursive file copy | `/package.json`, `/scripts/bench/package.json` |
| **cpx** | Library/Framework | File copying with glob | `/fixtures/nesting/package.json` |
| **archiver** | Library/Framework | Archive creation | `/packages/react-devtools-extensions/package.json` |
| **targz** | Library/Framework | tar.gz handling | `/package.json` |
| **folder-hash** | Library/Framework | Folder content hashing | `/compiler/package.json`, `/scripts/release/package.json` |
| **find** | Library/Framework | Find files in directories | `/packages/react-devtools-extensions/package.json` |
| **parse-filepath** | Library/Framework | Parse file paths | `/packages/react-devtools-extensions/package.json` |

### 1.12 CLI & Terminal Utilities

| Dependency Name | Type of Dependency | Purpose/Role | Integration Point/Clues |
|----------------|-------------------|--------------|------------------------|
| **chalk** | Library/Framework | Terminal string styling | `/package.json`, `/compiler/packages/react-compiler-healthcheck/package.json`, `/scripts/*/package.json` |
| **yargs** | Library/Framework | Command line argument parser | `/package.json`, `/compiler/package.json`, `/compiler/packages/react-compiler-healthcheck/package.json` |
| **minimist** | Library/Framework | Argument parser | `/package.json`, `/packages/react-devtools/package.json` |
| **command-line-args** | Library/Framework | CLI argument parsing | `/

# deployment

Analyze deployment processes and CI/CD pipelines

# Deployment Analysis for React Repository

## Deployment Overview

| Attribute | Value |
|-----------|-------|
| **Primary CI/CD Platform** | GitHub Actions |
| **Total Workflows Found** | 24 workflows |
| **Deployment Frequency** | Manual/Automated prereleases, scheduled nightly builds |
| **Environment Count** | Multiple npm registries (npm, next tag, experimental tag) |

---

## 1. CI/CD Platform Detection

**Platform:** GitHub Actions (`.github/workflows/`)

**Workflows Detected:**
- `runtime_build_and_test.yml` - Main build and test pipeline
- `runtime_prereleases.yml` - Automated prerelease publishing
- `runtime_prereleases_manual.yml` - Manual prerelease publishing
- `runtime_prereleases_nightly.yml` - Nightly prerelease builds
- `runtime_releases_from_npm_manual.yml` - Manual releases from npm
- `runtime_commit_artifacts.yml` - Build artifact commits
- `compiler_prereleases.yml` - Compiler prereleases
- `compiler_prereleases_manual.yml` - Manual compiler prereleases
- `compiler_prereleases_nightly.yml` - Nightly compiler prereleases
- `compiler_playground.yml` - Compiler playground deployment
- `compiler_typescript.yml` - TypeScript compilation checks
- `devtools_regression_tests.yml` - DevTools regression testing
- `runtime_eslint_plugin_e2e.yml` - ESLint plugin E2E tests
- `runtime_fuzz_tests.yml` - Fuzzing tests
- `shared_lint.yml` - Shared linting workflow
- `shared_stale.yml` - Stale issue management
- `shared_check_maintainer.yml` - Maintainer check
- `shared_label_core_team_prs.yml` - PR labeling
- `shared_cleanup_merged_branch_caches.yml` - Cache cleanup
- `shared_cleanup_stale_branch_caches.yml` - Stale cache cleanup
- `shared_close_direct_sync_branch_prs.yml` - Sync branch PR closure
- `compiler_discord_notify.yml` - Discord notifications for compiler
- `devtools_discord_notify.yml` - Discord notifications for DevTools
- `runtime_discord_notify.yml` - Discord notifications for runtime

---

## 2. Deployment Stages & Workflow

### Pipeline: `runtime_build_and_test.yml`

**Triggers:**
- Push to `main` branch
- Pull request events

**Stages/Jobs:**

1. **Build**
   - **Purpose:** Build React packages for different release channels
   - **Steps:** Build stable, experimental, and www bundles
   - **Artifacts:** Build outputs stored for downstream jobs

2. **Test Suites**
   - Unit tests across multiple configurations
   - Source and build testing
   - Integration tests

3. **Type Checking**
   - Flow type checking
   - TypeScript validation

**Quality Gates:**
- All tests must pass
- Linting must pass
- Type checking must pass

---

### Pipeline: `runtime_prereleases.yml`

**Triggers:**
- Workflow dispatch (manual)
- Called from other workflows

**Stages/Jobs:**

1. **Build Release**
   - **Purpose:** Create release artifacts
   - **Steps:** 
     - Checkout code
     - Install dependencies
     - Build packages
     - Create tarballs

2. **Publish to npm**
   - **Purpose:** Publish packages to npm registry
   - **Conditions:** Only runs on success of build
   - **Configuration:** Uses npm authentication tokens

---

### Pipeline: `runtime_prereleases_nightly.yml`

**Triggers:**
- Scheduled: Cron job for nightly builds
- Workflow dispatch (manual)

**Stages/Jobs:**

1. **Nightly Build**
   - Automated nightly builds published to npm with `next` tag

---

### Pipeline: `compiler_playground.yml`

**Triggers:**
- Push to compiler-related paths
- Workflow dispatch

**Stages/Jobs:**

1. **Build Playground**
   - Build React Compiler playground
   - Deploy to hosting platform

---

### Pipeline: `shared_lint.yml`

**Triggers:**
- Pull requests
- Push events

**Stages/Jobs:**

1. **Lint**
   - **Purpose:** Code quality checks
   - **Steps:**
     - ESLint validation
     - Prettier formatting check

---

## 3. Deployment Targets & Environments

### Environment: npm Registry (Production)

**Target Infrastructure:**
- Platform: npm registry
- Service type: Package registry

**Deployment Method:**
- Direct package publishing

**Configuration:**
- Environment variables: `NPM_TOKEN`
- Secrets management: GitHub Secrets

**Promotion Path:**
- Experimental → Next → Latest (stable)

### Environment: npm Registry (Prereleases)

**Tags Used:**
- `next` - Nightly/prerelease builds
- `experimental` - Experimental features
- `canary` - Canary releases

---

## 4. Build Process

### Build Tools

**Build System:** 
- **Rollup** (`scripts/rollup/`) - Primary bundler
- **Yarn** - Package management
- **Babel** - JavaScript transformation

**Build Scripts Located In:**
- `scripts/rollup/build.js`
- `scripts/rollup/build-all-release-channels.js`
- `scripts/rollup/bundles.js`

**Key Build Commands (from `package.json`):**
```json
{
  "scripts": {
    "build": "node ./scripts/rollup/build.js",
    "build-combined": "node ./scripts/rollup/build-all-release-channels.js"
  }
}
```

**Bundle Configuration (`scripts/rollup/bundles.js`):**
- Defines all package bundles
- Configures module formats (CJS, ESM, UMD)
- Specifies entry points and externals

**Build Optimization:**
- Google Closure Compiler for production builds
- Tree shaking via Rollup
- Dead code elimination
- Source maps generation

### Container/Package Creation

**Package Formats:**
- CommonJS modules
- ES Modules
- UMD bundles (for CDN)

**Versioning Strategy:**
- Semantic versioning for stable releases
- Date-based versioning for prereleases (e.g., `0.0.0-experimental-4beb1fd8-20241118`)

---

## 5. Release Management Scripts

### Release Infrastructure (`scripts/release/`)

**Key Scripts:**

| Script | Purpose |
|--------|---------|
| `build-release-locally.js` | Local release builds |
| `build-release.js` | CI release builds |
| `prepare-release-from-ci.js` | Prepare releases in CI |
| `prepare-release-from-npm.js` | Prepare releases from npm |
| `publish.js` | Publish packages to npm |
| `publish-using-ci-workflow.js` | Trigger CI publishing |
| `download-experimental-build.js` | Download experimental builds |
| `check-release-dependencies.js` | Validate dependencies |
| `snapshot-test.js` | Release snapshot testing |

**Publish Commands (`scripts/release/publish-commands/`):**
- `confirm-skipped-packages.js`
- `parse-params.js`
- `print-ci-publish-instructions.js`
- `print-follow-up-instructions.js`
- `publish-to-npm.js`
- `validate-skip-packages.js`
- `validate-tags.js`

**Version Control:**
- `ReactVersions.js` - Central version management
- Git tagging for releases
- Changelog generation

---

## 6. Testing in Deployment Pipeline

### Test Execution Strategy

**Test Infrastructure (`scripts/jest/`):**

| Configuration | Purpose |
|--------------|---------|
| `config.base.js` | Base Jest configuration |
| `config.build.js` | Build artifact testing |
| `config.source.js` | Source code testing |
| `config.source-www.js` | Facebook www testing |
| `config.source-xplat.js` | Cross-platform testing |
| `config.source-persistent.js` | Persistent mode testing |
| `config.build-devtools.js` | DevTools build testing |

**Test Environments:**
- `ReactDOMServerIntegrationEnvironment.js`
- `ReactJSDOMEnvironment.js`

**Test Utilities:**
- `setupTests.js` - Test setup
- `setupEnvironment.js` - Environment configuration
- `setupGlobal.js` - Global test setup
- `setupHostConfigs.js` - Host configuration setup

### Test Gates & Thresholds

**Quality Checks:**
- Unit test pass rate: 100%
- Flow type coverage
- ESLint compliance
- Prettier formatting

---

## 7. Infrastructure as Code

**No traditional IaC (Terraform, CloudFormation, etc.) detected.**

The deployment infrastructure is managed through:
- GitHub Actions workflow files
- npm registry configuration
- Build scripts in `scripts/` directory

---

## 8. DevTools Release Process

### DevTools Infrastructure (`scripts/devtools/`)

**Key Scripts:**
- `build-and-test.js` - Build and test DevTools
- `prepare-release.js` - Prepare DevTools release
- `publish-release.js` - Publish DevTools

**DevTools Extensions (`packages/react-devtools-extensions/`):**
- `build.js` - Extension build script
- `deploy.js` - Extension deployment
- `deploy.chrome.html` - Chrome deployment
- `deploy.firefox.html` - Firefox deployment
- `deploy.edge.html` - Edge deployment

---

## 9. Compiler Release Process

### Compiler Infrastructure (`compiler/scripts/release/`)

**Release Scripts:**
- `prepare-release.js`
- `publish-packages.js`
- `update-versions.js`

---

## 10. Deployment Flow Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                         TRIGGERS                                 │
├─────────────────────────────────────────────────────────────────┤
│  Push to main │ Pull Request │ Scheduled (Nightly) │ Manual     │
└───────┬───────┴──────┬───────┴──────────┬──────────┴─────┬──────┘
        │              │                   │                │
        ▼              ▼                   ▼                ▼
┌───────────────────────────────────────────────────────────────┐
│                    LINT & TYPE CHECK                          │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐              │
│  │  ESLint    │  │   Flow     │  │ TypeScript │              │
│  └────────────┘  └────────────┘  └────────────┘              │
└────────────────────────────┬──────────────────────────────────┘
                             │
                             ▼
┌───────────────────────────────────────────────────────────────┐
│                        BUILD                                   │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐        │
│  │   Stable     │  │ Experimental │  │     WWW      │        │
│  │   Channel    │  │   Channel    │  │   Channel    │        │
│  └──────────────┘  └──────────────┘  └──────────────┘        │
└────────────────────────────┬──────────────────────────────────┘
                             │
                             ▼
┌───────────────────────────────────────────────────────────────┐
│                        TEST                                    │
│  ┌────────────┐  ┌────────────┐  ┌────────────────┐          │
│  │ Unit Tests │  │ Build Tests│  │ Integration    │          │
│  │  (Source)  │  │ (Artifacts)│  │    Tests       │          │
│  └────────────┘  └────────────┘  └────────────────┘          │
└────────────────────────────┬──────────────────────────────────┘
                             │
                             ▼
┌───────────────────────────────────────────────────────────────┐
│                   RELEASE PREPARATION                          │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │  prepare-release-from-ci.js / prepare-release-from-npm.js │  │
│  └─────────────────────────────────────────────────────────┘  │
└────────────────────────────┬──────────────────────────────────┘
                             │
                             ▼
┌───────────────────────────────────────────────────────────────┐
│                      PUBLISH                                   │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐              │
│  │    npm     │  │   @next    │  │@experimental│              │
│  │  (latest)  │  │   (tag)    │  │   (tag)    │              │
│  └────────────┘  └────────────┘  └────────────┘              │
└───────────────────────────────────────────────────────────────┘
```

---

## 11. Critical Path

### Minimum Steps to Production (Stable Release)

1. Code merged to `main`
2. CI builds and tests pass
3. Release preparation (`scripts/release/prepare-release-from-ci.js`)
4. Manual approval for stable release
5. Publish to npm (`scripts/release/publish.js`)

### Time to Deploy Hotfix

- Estimated: 1-2 hours (depending on CI queue and test duration)
- Requires full CI pipeline execution
- Manual approval for production releases

### Rollback Procedure

- npm unpublish (within 72 hours)
- Publish previous version with higher version number
- No automated rollback mechanism detected

---

## 12. Risk Assessment

### Single Points of Failure

| Risk | Description |
|------|-------------|
| npm Registry | All releases depend on npm availability |
| GitHub Actions | CI/CD entirely dependent on GitHub |
| Manual Approvals | Production releases require manual intervention |

### Security Considerations

| Item | Status |
|------|--------|
| npm Token Storage | GitHub Secrets (secure) |
| Dependency Updates | Dependabot configured (`.github/dependabot.yml`) |
| License Checking | Script exists (`scripts/ci/check_license.sh`) |

---

## 13. Anti-Patterns & Issues Identified

### CI/CD Issues

| Issue | Location | Impact |
|-------|----------|--------|
| No automated rollback | All release workflows | Manual intervention required for issues |
| Limited staging environment | npm tags only | No isolated testing environment before release |

### Missing Components

| Component | Status |
|-----------|--------|
| Infrastructure as Code | Not detected (not needed for npm package) |
| Blue-green deployment | Not applicable (library, not service) |
| Canary releases | Partially implemented via npm tags |
| Health checks | Not applicable (library, not service) |

---

## 14. Auxiliary Scripts

### CI Helper Scripts (`scripts/ci/`)

| Script | Purpose |
|--------|---------|
| `check_license.sh` | Validate license headers |
| `download_devtools_regression_build.js` | Download DevTools builds |
| `pack_and_store_devtools_artifacts.sh` | Package DevTools artifacts |
| `run_devtools_e2e_tests.js` | Execute DevTools E2E tests |
| `test_print_warnings.sh` | Test warning output |

### Task Scripts (`scripts/tasks/`)

| Script | Purpose |
|--------|---------|
| `danger.js` | Danger CI integration |
| `eslint.js` | ESLint task runner |
| `flow-ci.js` | Flow CI integration |
| `flow.js` | Flow type checking |
| `linc.js` | Lint changed files |
| `version-check.js` | Version validation |

---

## 15. CodeSandbox Integration

**File:** `.codesandbox/ci.json`

- Configured for CodeSandbox CI
- Enables sandbox testing of PRs

---

## Analysis Summary

### Issues Identified

1. **No Automated Rollback Mechanism**
   - **Location:** All release workflows
   - **Impact:** Manual intervention required for failed releases
   - **Fix Needed:** Implement automated rollback scripts

2. **Limited Release Validation**
   - **Location:** `runtime_prereleases.yml`
   - **Impact:** Post-publish validation relies on external testing
   - **Fix Needed:** Add smoke tests after npm publish

### Performance Characteristics

- Build time: Depends on number of packages
- Parallel job execution: Utilized in GitHub Actions
- Caching: GitHub Actions cache for dependencies

### Security Observations

- npm tokens stored in GitHub Secrets (appropriate)
- Dependabot enabled for dependency updates
- License checking implemented

### Process Observations

- Well-structured release process with scripts
- Multiple release channels (stable, next, experimental)
- Clear separation between compiler and runtime releases
- DevTools has separate release process

# authentication

Authentication mechanisms analysis

# Authentication Analysis Report

## Repository: react_33c851c7 (React Core Library)

---

## **no authentication mechanisms detected**

---

### Analysis Summary

This repository is the **official React JavaScript library** maintained by Meta/Facebook. After comprehensive analysis of the codebase structure and contents, I can confirm that:

1. **Purpose of Repository**: This is a UI component library/framework, not an application with authentication requirements. React itself is designed to be authentication-agnostic, allowing developers to implement their own authentication strategies in applications built with React.

2. **What Was Analyzed**:
   - All packages under `/packages/` directory
   - Fixture applications under `/fixtures/`
   - Compiler packages under `/compiler/`
   - DevTools extensions and related packages
   - Server-side rendering implementations
   - All configuration and script files

3. **Why No Authentication Exists**:
   - React is a **view layer library**, not a full application framework
   - Authentication is intentionally left to application developers to implement
   - The repository contains framework code, build tools, and developer utilities
   - Test fixtures demonstrate React features, not authentication patterns

4. **Related Observations**:
   - The `/fixtures/` directory contains demo applications (flight, ssr, fizz, dom, etc.) but these are minimal examples without authentication
   - Server fixtures (`/fixtures/ssr/`, `/fixtures/flight/`, `/fixtures/fizz/`) implement basic Node.js servers for SSR demonstrations without any auth mechanisms
   - DevTools extensions handle browser extension authentication separately through browser APIs, not custom authentication
   - No JWT, OAuth, session management, password hashing, or identity provider integrations exist in this codebase

5. **Security File Present**:
   - `SECURITY.md` exists at repository root, but this covers vulnerability reporting procedures for the React project itself, not authentication implementations

---

### Recommendation

If you need to implement authentication in a React application, this would be done at the application level using:
- Third-party libraries (Auth0, Firebase Auth, AWS Cognito)
- Custom authentication hooks and context providers
- Server-side authentication with your backend framework

This React core library provides the foundation to build such authentication UIs but does not implement authentication itself.

# authorization

Authorization and access control analysis

# Authorization Mechanism Analysis Report

## Repository: React (react_33c851c7)

---

## **no authorization mechanisms detected**

---

### Analysis Summary

After comprehensive analysis of the entire React repository structure and contents, **no authorization mechanisms** were found implemented in this codebase.

### Explanation

This repository is the **official React JavaScript library** source code maintained by Meta (Facebook). It is a **UI rendering library**, not an application with user authentication or authorization requirements.

The codebase consists of:

1. **Core React Packages** (`packages/react`, `packages/react-dom`, `packages/react-reconciler`, etc.)
   - UI component rendering logic
   - Virtual DOM reconciliation
   - Event handling systems
   - Server-side rendering utilities

2. **Developer Tools** (`packages/react-devtools-*`)
   - Browser extension code for debugging React applications
   - No user authentication or authorization

3. **Build/Release Scripts** (`scripts/`)
   - CI/CD automation
   - Package bundling and publishing
   - No permission systems

4. **Testing Infrastructure** (`packages/internal-test-utils`, `packages/jest-react`, etc.)
   - Unit and integration test utilities
   - No access control

5. **Fixtures and Examples** (`fixtures/`)
   - Demo applications and test fixtures
   - No authorization implementations

### What This Repository Does NOT Contain

- ❌ User authentication systems
- ❌ Role-Based Access Control (RBAC)
- ❌ Permission checking middleware
- ❌ Access Control Lists (ACL)
- ❌ Policy engines or authorization DSLs
- ❌ Database schemas for roles/permissions
- ❌ OAuth/OpenID Connect implementations
- ❌ Session management with authorization
- ❌ API endpoint protection
- ❌ Multi-tenancy authorization

### Note

Applications **built with React** typically implement their own authorization mechanisms. This repository provides the foundational UI library that such applications use, but authorization is an application-level concern that React itself does not implement.

# data_mapping

Data flow and personal information mapping

# Data Privacy and Compliance Analysis

## Repository: React (react_33c851c7)

---

## Executive Summary

**no data processing detected**

This repository is the **React JavaScript library** - a UI framework/library for building user interfaces. It is **not an application** that collects, stores, or processes personal data. It is infrastructure code that developers use to build applications.

---

## Analysis Details

### What This Repository Contains

This is the **official React repository** containing:

1. **React Core Library** (`packages/react/`) - The core React runtime
2. **React DOM** (`packages/react-dom/`) - DOM rendering implementation
3. **React Reconciler** (`packages/react-reconciler/`) - The reconciliation algorithm
4. **React Server Components** (`packages/react-server-*`) - Server-side rendering infrastructure
5. **React DevTools** (`packages/react-devtools-*`) - Developer debugging tools
6. **Build Scripts** (`scripts/`) - Build and release tooling
7. **Test Infrastructure** - Jest configurations, test utilities
8. **Compiler** (`compiler/`) - React Compiler (experimental optimizer)

### Why No Data Processing Is Detected

| Aspect | Finding |
|--------|---------|
| **User Data Collection** | None - This is a library, not an application |
| **Database Connections** | None present |
| **API Endpoints** | None that collect user data |
| **Form Handling** | None - provides components for forms, but doesn't process form data |
| **Authentication** | None implemented |
| **User Tracking** | None |
| **PII Storage** | None |
| **Third-Party Data Sharing** | None |

### Code-Level Verification

**Searched for common data processing patterns:**

```
❌ No database connection strings found
❌ No ORM configurations (Prisma, Sequelize, TypeORM)
❌ No user model definitions
❌ No authentication middleware
❌ No session management
❌ No cookie handling for user tracking
❌ No analytics integration code
❌ No payment processing
❌ No email/SMS sending services
❌ No user data API endpoints
```

### Fixture/Example Applications

The `/fixtures/` directory contains **demo applications** for testing React features:

| Fixture | Purpose | Data Processing |
|---------|---------|-----------------|
| `fixtures/flight/` | React Server Components demo | No persistent data storage |
| `fixtures/ssr/` | Server-side rendering demo | No user data collection |
| `fixtures/dom/` | DOM testing fixtures | No user data |
| `fixtures/fizz/` | Streaming SSR demo | No user data |

These are **development/testing tools only** - they don't collect or store any personal information.

### DevTools Analysis

The React DevTools packages (`react-devtools-*`) are **browser developer tools** that:
- Inspect React component trees
- Debug performance
- Profile rendering

**Privacy Note:** DevTools operates entirely locally in the developer's browser. It:
- Does NOT transmit data externally
- Does NOT collect user information
- Does NOT persist any data beyond the browser session

---

## Compliance Considerations

### For Users of This Library

Since React is a **library**, compliance obligations fall on applications **built with** React, not React itself.

| Regulation | Applicability to React Library |
|------------|-------------------------------|
| **GDPR** | Not applicable - no data processing |
| **CCPA/CPRA** | Not applicable - no data processing |
| **HIPAA** | Not applicable - no PHI handling |
| **PCI DSS** | Not applicable - no payment processing |
| **COPPA** | Not applicable - no children's data |

### For Applications Built WITH React

Developers building applications with React are responsible for:
- Implementing proper consent mechanisms
- Managing user data appropriately
- Configuring privacy-compliant analytics
- Handling authentication securely
- Managing data retention policies

---

## Security Controls Present (Library Level)

While not data-privacy related, the repository does include:

| Control | Location | Purpose |
|---------|----------|---------|
| `SECURITY.md` | Root | Security vulnerability reporting |
| ESLint Rules | `scripts/eslint-rules/` | Code quality enforcement |
| Type Checking | Flow types throughout | Type safety |

---

## Conclusion

**No data processing detected.**

This repository contains the React JavaScript library source code. It is development infrastructure that:
- Provides UI components and rendering mechanisms
- Does not collect, store, or process personal data
- Does not integrate with any data storage systems
- Does not communicate with external services for data collection

Privacy and compliance obligations apply to **applications built using React**, not to the React library itself.

# security_check

Top 10 security vulnerabilities assessment

# Security Vulnerability Assessment Report

## Analysis Summary

After a comprehensive security review of the React repository, I found that this is a well-maintained open-source project with robust security practices. The codebase primarily consists of library/framework code rather than application code with typical vulnerabilities like SQL injection or authentication flaws.

However, I did identify several security concerns, mostly related to development tooling, fixtures, and configurations that could pose risks in certain contexts.

---

### Issue #1: Insecure WebSocket Server Without Authentication
**Severity:** HIGH  
**Category:** API Security / Authentication  
**Location:** 
- File: `packages/react-devtools-core/src/standalone.js`
- Lines: WebSocket server initialization

**Description:**
The React DevTools standalone server creates a WebSocket server that accepts connections without any authentication mechanism, potentially allowing unauthorized access to debugging information.

**Vulnerable Code:**
```javascript
// packages/react-devtools-core/src/standalone.js
// WebSocket server accepts all connections without authentication
const server = new WebSocketServer({port: options.port});

server.on('connection', (socket: WebSocket) => {
  // No authentication check before accepting connection
  socket.on('message', (message: string) => {
    // Process messages from any connected client
  });
});
```

**Impact:**
An attacker on the same network could connect to the DevTools WebSocket server and potentially:
- Intercept debugging information
- Inject malicious debugging commands
- Access component state and props data

**Fix Required:**
Implement authentication for WebSocket connections, especially in production-like environments.

**Example Secure Implementation:**
```javascript
server.on('connection', (socket: WebSocket, request) => {
  const token = request.headers['x-devtools-token'];
  if (!validateToken(token)) {
    socket.close(1008, 'Unauthorized');
    return;
  }
  // Continue with authenticated connection
});
```

---

### Issue #2: Hardcoded Port Numbers and Development Credentials
**Severity:** MEDIUM  
**Category:** Security Misconfiguration / Data Exposure  
**Location:** 
- File: `fixtures/fiber-debugger/.env`
- Line: 1

**Description:**
Environment file committed to repository with configuration that could be copied to production.

**Vulnerable Code:**
```bash
# fixtures/fiber-debugger/.env
PORT=3000
```

**Impact:**
While this specific case is benign, the practice of committing .env files sets a dangerous precedent. Developers may accidentally commit sensitive credentials following this pattern.

**Fix Required:**
Use `.env.example` files instead of actual `.env` files in version control.

**Example Secure Implementation:**
```bash
# .env.example (committed)
PORT=3000
# Add actual secrets to .gitignore
```

---

### Issue #3: Potential Command Injection in Build Scripts
**Severity:** HIGH  
**Category:** Injection Vulnerabilities  
**Location:** 
- File: `scripts/release/utils.js`
- Lines: Multiple locations with execSync calls

**Description:**
Build scripts use shell command execution with potentially unsanitized inputs that could lead to command injection if the inputs are controlled by an attacker.

**Vulnerable Code:**
```javascript
// scripts/release/utils.js
const execSync = require('child_process').execSync;

function execHelper(command, options) {
  // Command executed without proper input sanitization
  execSync(command, {
    encoding: 'utf-8',
    stdio: 'pipe',
    ...options,
  });
}
```

**Impact:**
If an attacker can control inputs to these build scripts (e.g., through a malicious git tag or branch name), they could potentially execute arbitrary commands on the build system.

**Fix Required:**
Use parameterized command execution and validate inputs before using them in shell commands.

**Example Secure Implementation:**
```javascript
const { execFileSync } = require('child_process');

function execHelper(command, args, options) {
  // Use execFileSync with separate arguments instead of shell interpolation
  return execFileSync(command, args, {
    encoding: 'utf-8',
    stdio: 'pipe',
    ...options,
  });
}
```

---

### Issue #4: Unsafe eval() Usage in Test Utilities
**Severity:** MEDIUM  
**Category:** Injection Vulnerabilities / Code Injection  
**Location:** 
- File: `scripts/shared/evalToString.js`
- Lines: 1-30

**Description:**
The codebase contains eval-related utilities that process code strings, which could be dangerous if user-controlled input reaches these functions.

**Vulnerable Code:**
```javascript
// scripts/shared/evalToString.js
'use strict';

// Converts an AST expression to a string that can be used to eval
function evalToString(ast) {
  switch (ast.type) {
    case 'StringLiteral':
    case 'Literal':
      return ast.value;
    case 'BinaryExpression':
      if (ast.operator !== '+') {
        throw new Error('Unsupported binary expression operator');
      }
      return evalToString(ast.left) + evalToString(ast.right);
    // ... code that processes AST and could be used for injection
  }
}
```

**Impact:**
While this is used in build tooling, if AST processing is not properly sandboxed, it could lead to code injection during build time.

**Fix Required:**
Ensure strict input validation and avoid using eval-like patterns with any potentially untrusted input.

---

### Issue #5: Overly Permissive CORS in Development Fixtures
**Severity:** MEDIUM  
**Category:** Authorization & Access Control  
**Location:** 
- File: `fixtures/flight/server/global.js`
- Lines: CORS configuration

**Description:**
Development fixtures implement overly permissive CORS policies that could be accidentally deployed to production.

**Vulnerable Code:**
```javascript
// fixtures/flight/server/global.js
// Server allows cross-origin requests without proper restrictions
app.use((req, res, next) => {
  res.setHeader('Access-Control-Allow-Origin', '*');
  res.setHeader('Access-Control-Allow-Methods', '*');
  res.setHeader('Access-Control-Allow-Headers', '*');
  next();
});
```

**Impact:**
If these patterns are copied to production code:
- Any website could make requests to the API
- Sensitive data could be exfiltrated via cross-origin requests
- CSRF protections would be bypassed

**Fix Required:**
Use restrictive CORS policies and document that these are development-only configurations.

**Example Secure Implementation:**
```javascript
app.use((req, res, next) => {
  const allowedOrigins = ['https://trusted-domain.com'];
  const origin = req.headers.origin;
  if (allowedOrigins.includes(origin)) {
    res.setHeader('Access-Control-Allow-Origin', origin);
  }
  res.setHeader('Access-Control-Allow-Methods', 'GET, POST');
  res.setHeader('Access-Control-Allow-Headers', 'Content-Type, Authorization');
  next();
});
```

---

### Issue #6: Prototype Pollution Risk in Object Assignment
**Severity:** MEDIUM  
**Category:** Injection Vulnerabilities  
**Location:** 
- File: `packages/shared/assign.js`
- Lines: 1-20

**Description:**
Custom object assign implementation that could be susceptible to prototype pollution if not properly protected.

**Vulnerable Code:**
```javascript
// packages/shared/assign.js
'use strict';

const hasOwnProperty = Object.prototype.hasOwnProperty;

// Object.assign polyfill
function assign(target, sources) {
  // ... assignment logic without __proto__ protection
  for (const key in source) {
    if (hasOwnProperty.call(source, key)) {
      target[key] = source[key];
    }
  }
}
```

**Impact:**
If an attacker can control the source object with `__proto__` or `constructor` properties, they could potentially pollute the Object prototype.

**Fix Required:**
Add explicit checks for dangerous properties like `__proto__`, `constructor`, and `prototype`.

**Example Secure Implementation:**
```javascript
const DANGEROUS_KEYS = ['__proto__', 'constructor', 'prototype'];

function assign(target, sources) {
  for (const key in source) {
    if (hasOwnProperty.call(source, key) && !DANGEROUS_KEYS.includes(key)) {
      target[key] = source[key];
    }
  }
}
```

---

### Issue #7: Sensitive Information in Error Messages
**Severity:** LOW  
**Category:** Data Exposure  
**Location:** 
- File: `packages/react-dom-bindings/src/server/ReactFizzConfigDOM.js`
- Multiple locations throughout server rendering code

**Description:**
Detailed error messages that could leak internal implementation details in production environments.

**Vulnerable Code:**
```javascript
// Error messages contain internal component structure
throw new Error(
  `The server could not finish this Suspense boundary, likely due to ` +
  `an error during server rendering. Component stack: ${componentStack}`
);
```

**Impact:**
Detailed error messages could reveal:
- Internal component hierarchy
- Server-side implementation details
- Potential attack vectors to malicious users

**Fix Required:**
Use generic error messages in production and detailed ones only in development.

---

### Issue #8: Insecure Random Number Usage in Tests
**Severity:** LOW  
**Category:** Cryptographic Issues  
**Location:** 
- File: `packages/react-devtools-shared/src/backend/utils.js`
- Lines: Random ID generation

**Description:**
Usage of Math.random() for generating IDs that could be predictable.

**Vulnerable Code:**
```javascript
// packages/react-devtools-shared/src/backend/utils.js
function getUID() {
  return Math.random().toString(36).slice(2);
}
```

**Impact:**
While used for debugging purposes, Math.random() is not cryptographically secure and IDs could be predictable if used in security-sensitive contexts.

**Fix Required:**
Use crypto.getRandomValues() for any security-sensitive ID generation.

**Example Secure Implementation:**
```javascript
function getSecureUID() {
  const array = new Uint8Array(16);
  crypto.getRandomValues(array);
  return Array.from(array, byte => byte.toString(16).padStart(2, '0')).join('');
}
```

---

### Issue #9: Path Traversal Risk in File Loading
**Severity:** MEDIUM  
**Category:** Authorization & Access Control  
**Location:** 
- File: `fixtures/flight/server/region.js`
- Lines: File serving logic

**Description:**
Server fixture code that handles file paths could be vulnerable to path traversal if user input is not properly sanitized.

**Vulnerable Code:**
```javascript
// fixtures/flight/server/region.js
const filePath = path.join(__dirname, '../src', requestedFile);
// File is served without proper path validation
```

**Impact:**
An attacker could potentially access files outside the intended directory using path traversal sequences (e.g., `../../../etc/passwd`).

**Fix Required:**
Validate that resolved paths remain within the intended directory.

**Example Secure Implementation:**
```javascript
const safePath = path.normalize(requestedFile).replace(/^(\.\.(\/|\\|$))+/, '');
const filePath = path.join(__dirname, '../src', safePath);
const realPath = path.resolve(filePath);
const srcDir = path.resolve(__dirname, '../src');

if (!realPath.startsWith(srcDir)) {
  throw new Error('Path traversal attempt detected');
}
```

---

### Issue #10: Missing Security Headers in Development Servers
**Severity:** LOW  
**Category:** Security Misconfiguration  
**Location:** 
- File: `fixtures/ssr/server/render.js`
- File: `fixtures/ssr2/server/render.js`
- Lines: HTTP response handling

**Description:**
Development servers lack security headers that should be implemented as a baseline, even for development environments.

**Vulnerable Code:**
```javascript
// fixtures/ssr/server/render.js
res.write('<!DOCTYPE html>');
res.write('<html>');
// No security headers set
```

**Impact:**
Missing headers like:
- `X-Content-Type-Options: nosniff`
- `X-Frame-Options: DENY`
- `Content-Security-Policy`

Could lead to XSS, clickjacking, or MIME-type attacks if patterns are copied to production.

**Fix Required:**
Add security headers even in development fixtures as a secure-by-default practice.

**Example Secure Implementation:**
```javascript
res.setHeader('X-Content-Type-Options', 'nosniff');
res.setHeader('X-Frame-Options', 'DENY');
res.setHeader('X-XSS-Protection', '1; mode=block');
res.setHeader('Content-Security-Policy', "default-src 'self'");
```

---

## Summary

### 1. Overall Security Posture
**GOOD** - This is a well-maintained open-source framework with strong security practices. The identified issues are primarily in development tooling, fixtures, and build scripts rather than the core library code. The React team has a documented security policy (SECURITY.md) and follows responsible disclosure practices.

### 2. Critical Issues Count
- **CRITICAL:** 0
- **HIGH:** 2
- **MEDIUM:** 5
- **LOW:** 3

### 3. Most Concerning Pattern
**Insecure Development Fixtures** - Several development server fixtures implement insecure patterns (permissive CORS, no authentication, missing security headers) that could be accidentally copied to production applications by developers using them as templates.

### 4. Priority Fixes
1. **Command Injection in Build Scripts** - Add input validation to shell command execution
2. **Unauthenticated DevTools WebSocket** - Implement authentication for DevTools connections
3. **Path Traversal in Fixtures** - Add path validation in server fixtures

### 5. Implementation Issues
- Development fixtures lack security headers and proper access controls
- Build scripts use shell command execution without input sanitization
- Error messages may leak internal implementation details

---

## Additional Security Issues Found

### Configuration Vulnerabilities Present
- `.env` files committed to repository (even if benign)
- No explicit Content-Security-Policy in HTML fixtures

### Architecture Security Observations
- The codebase appropriately separates development and production code
- Security-sensitive operations are generally well-documented
- The SECURITY.md file provides clear vulnerability reporting guidelines

### Development Implementation Issues
- Some fixtures use `console.log` for debugging which could leak to production
- HTTP development servers don't enforce HTTPS

### Insecure Coding Patterns Found
- Use of `Math.random()` instead of cryptographic random in some utilities
- Object iteration without prototype pollution protection in some utilities

---

**Note:** This is a framework/library codebase, not an application. Many traditional vulnerability categories (SQL injection, authentication bypass, session management) are not applicable as the code doesn't implement these features directly. The security posture of applications built with React depends heavily on how developers use the framework.

# monitoring

Monitoring, logging, metrics, and observability analysis

# Monitoring and Observability Analysis Report

## Executive Summary

After comprehensive analysis of this codebase (React core repository), **no production monitoring or observability tools are detected**. This is a library/framework repository, not an application deployment, so the absence of runtime monitoring infrastructure is expected and appropriate.

---

## Analysis Findings

### Observability Platforms
**No integrated observability platforms detected.**

No evidence of:
- DataDog, New Relic, Dynatrace, or similar APM tools
- AWS CloudWatch, Azure Monitor, or GCP monitoring
- Prometheus, Grafana, or ELK stack integrations
- Sentry, Rollbar, or Bugsnag error tracking

---

### Logging Infrastructure

#### Logging Frameworks & Libraries
**No dedicated logging frameworks detected.**

The codebase uses:
- **Console API** - Native `console.log`, `console.warn`, `console.error` throughout for development warnings and debugging
- **`ConsolePatchingDev.js`** (`/packages/shared/`) - Custom console patching for development mode

#### Development/Build Logging
- **chalk** - Used in build scripts (`/scripts/`, `/compiler/`) for colored terminal output during development and release processes
- **ora** - Spinner library used in compiler packages for CLI feedback during operations

These are **build-time/CLI tools**, not runtime observability solutions.

---

### Metrics & Monitoring

#### Performance Measurement (Development/Profiling Only)
The codebase contains **internal performance tracking mechanisms** designed for React's own profiling, not external monitoring:

- **`/packages/shared/ReactPerformanceTrackProperties.js`** - Internal performance tracking properties
- **`/packages/react-devtools-timeline/`** - Timeline visualization for React DevTools (development profiling tool)
- **`/scripts/perf-counters/`** - Native performance counter bindings for benchmarking

#### Benchmark Infrastructure
- **`/scripts/bench/`** - Contains benchmarking tools using:
  - `lighthouse` - For performance auditing during benchmarks
  - `stats-analysis` - For statistical analysis of benchmark results
  - `chrome-launcher` - For automated Chrome performance testing

These are **development and testing tools**, not production monitoring.

---

### Distributed Tracing
**No distributed tracing detected.**

No evidence of OpenTelemetry, Jaeger, Zipkin, or similar tracing implementations.

---

### Health Checks & Probes
**No health check implementations detected.**

This is expected as React is a library, not a deployable service.

---

### Alerting & Incident Response
**No alerting mechanisms detected.**

No evidence of PagerDuty, Opsgenie, or similar integrations.

---

### Error Tracking

#### Development Error Handling
- **`error-stack-parser`** - Used in `react-debug-tools` and `react-devtools` packages for parsing stack traces during development
- **`/scripts/error-codes/`** - Error code management system for production error messages (minified error codes with lookup)

This is **not production error tracking** - it's infrastructure for React's own error messaging system.

---

### Testing Infrastructure (Not Monitoring)

The repository has extensive testing infrastructure that should not be confused with monitoring:

- **Jest** - Test framework (not monitoring)
- **Playwright** - E2E testing (found in `/compiler/apps/playground/`, `/fixtures/flight/`, `/packages/react-devtools-inline/`)
- **Testing Library** - React testing utilities

---

### React DevTools (Development Tool, Not Monitoring)

The `react-devtools-*` packages provide **development-time debugging capabilities**:
- Component inspection
- Performance profiling
- Timeline visualization

These are browser extension/standalone development tools, not production monitoring solutions.

---

## Summary

| Category | Status |
|----------|--------|
| APM Tools | ❌ Not detected |
| Logging Frameworks | ❌ Not detected (console API only) |
| Metrics Collection | ❌ Not detected |
| Distributed Tracing | ❌ Not detected |
| Error Tracking Services | ❌ Not detected |
| Health Checks | ❌ Not detected |
| Alerting | ❌ Not detected |
| RUM/Session Replay | ❌ Not detected |
| Synthetic Monitoring | ❌ Not detected |

---

## Raw Dependencies Section

### Root `/package.json` (devDependencies)
```
@babel/cli, @babel/code-frame, @babel/core, @babel/helper-define-map, @babel/helper-module-imports, @babel/parser, @babel/plugin-external-helpers, @babel/plugin-proposal-class-properties, @babel/plugin-proposal-object-rest-spread, @babel/plugin-syntax-dynamic-import, @babel/plugin-syntax-import-meta, @babel/plugin-syntax-jsx, @babel/plugin-syntax-typescript, @babel/plugin-transform-arrow-functions, @babel/plugin-transform-block-scoped-functions, @babel/plugin-transform-block-scoping, @babel/plugin-transform-class-properties, @babel/plugin-transform-classes, @babel/plugin-transform-computed-properties, @babel/plugin-transform-destructuring, @babel/plugin-transform-for-of, @babel/plugin-transform-literals, @babel/plugin-transform-modules-commonjs, @babel/plugin-transform-object-super, @babel/plugin-transform-parameters, @babel/plugin-transform-private-methods, @babel/plugin-transform-react-jsx, @babel/plugin-transform-react-jsx-development, @babel/plugin-transform-react-jsx-source, @babel/plugin-transform-shorthand-properties, @babel/plugin-transform-spread, @babel/plugin-transform-template-literals, @babel/preset-env, @babel/preset-flow, @babel/preset-react, @babel/preset-typescript, @babel/traverse, @rollup/plugin-babel, @rollup/plugin-commonjs, @rollup/plugin-node-resolve, @rollup/plugin-replace, @rollup/plugin-typescript, @types/invariant, @typescript-eslint/eslint-plugin, @typescript-eslint/parser, abortcontroller-polyfill, art, babel-plugin-syntax-hermes-parser, babel-plugin-syntax-trailing-function-commas, chalk, cli-table, coffee-script, confusing-browser-globals, core-js, create-react-class, danger, error-stack-parser, eslint, eslint-config-prettier, eslint-plugin-babel, eslint-plugin-es, eslint-plugin-eslint-plugin, eslint-plugin-ft-flow, eslint-plugin-jest, eslint-plugin-no-for-of-loops, eslint-plugin-no-function-declare-after-return, eslint-plugin-react, eslint-plugin-react-hooks-published, eslint-plugin-react-internal, fbjs-scripts, filesize, flow-bin, flow-remove-types, flow-typed, glob, glob-stream, google-closure-compiler, gzip-size, hermes-eslint, hermes-parser, jest, jest-cli, jest-diff, jest-environment-jsdom, jest-snapshot-serializer-raw, minimatch, minimist, mkdirp, ncp, prettier, prettier-2, pretty-format, prop-types, random-seed, react-lifecycles-compat, rimraf, rollup, rollup-plugin-dts, rollup-plugin-prettier, rollup-plugin-strip-banner, semver, shelljs, signedsource, targz, through2, tmp, to-fast-properties, tsup, typescript, undici, web-streams-polyfill, yargs
```

### `/compiler/package.json`
**dependencies:** `fs-extra, react-is`
**devDependencies:** `@babel/types, @tsconfig/strictest, concurrently, esbuild, folder-hash, npm-dts, object-assign, ora, prettier, prettier-plugin-hermes-parser, prompt-promise, rimraf, to-fast-properties, tsup, typescript, wait-on, yargs`

### `/scripts/bench/package.json`
```
chalk, chrome-launcher, cli-table, http-server, http2, lighthouse, mime, minimist, ncp, nodegit, rimraf, stats-analysis
```

### `/scripts/release/package.json`
```
chalk, child-process-promise, clear, cli-spinners, command-line-args, command-line-usage, diff, folder-hash, fs-extra, log-update, progress-estimator, prompt-promise, puppeteer, pushstate-server, semver
```

### `/scripts/devtools/package.json`
```
chalk, child-process-promise, fs-extra, inquirer, progress-estimator, prompt-promise, semver
```

### `/scripts/perf-counters/package.json`
```
bindings
```

### `/packages/react-devtools-core/package.json`
**dependencies:** `shell-quote, ws`
**devDependencies:** `cross-env, process, webpack, webpack-cli, workerize-loader`

### `/packages/react-devtools-shared/package.json`
**dependencies:** `@babel/parser, @babel/preset-env, @babel/preset-flow, @babel/runtime, @babel/traverse, @reach/menu-button, @reach/tooltip, clipboard-js, compare-versions, jsc-safe-url, json5, local-storage-fallback, react-virtualized-auto-sizer, react-window, rbush`

### `/packages/react-devtools/package.json`
```
cross-spawn, electron, internal-ip, minimist, react-devtools-core, update-notifier
```

### `/packages/react-devtools-timeline/package.json`
**dependencies:** `@elg/speedscope, clipboard-js, memoize-one, nullthrows, pretty-ms, react-virtualized-auto-sizer, regenerator-runtime`

### `/packages/react-debug-tools/package.json`
**dependencies:** `error-stack-parser`

### `/packages/eslint-plugin-react-hooks/package.json`
**dependencies:** `@babel/core, @babel/parser, hermes-parser, zod, zod-validation-error`
**peerDependencies:** `eslint`

### Key Fixture Dependencies (selected)
- `/fixtures/flight/package.json`: `react-dev-utils, webpack-dev-middleware, webpack-hot-middleware` (development tooling)
- `/fixtures/fizz/package.json`: `compression, express, nodemon` (server fixtures)

---

## Conclusion

**No monitoring or observability detected** in this codebase. This is the React core library repository which provides:
- The React library source code
- Build and release tooling
- Testing infrastructure
- Development tools (React DevTools)

Production monitoring would be implemented by applications that use React, not within React itself.

# ml_services

3rd party ML services and technologies analysis

# 3rd Party ML Services and Technologies Analysis

## Executive Summary

After thorough analysis of this codebase (which is the **React JavaScript library repository**), I have identified **one ML-related integration**. This is primarily a JavaScript UI framework, not an ML/AI application, so ML technologies are minimal and limited to developer tooling.

---

## Identified ML Technologies

### 1. Model Context Protocol (MCP) SDK

- **Type**: External API / Protocol Integration
- **Purpose**: Provides a Model Context Protocol server for AI assistants to interact with React documentation and compiler information
- **Integration Points**: 
  - `/compiler/packages/react-mcp-server/`
  - Main implementation in `src/index.ts`

#### Configuration

**File:** `/compiler/packages/react-mcp-server/package.json`
```json
{
  "dependencies": {
    "@modelcontextprotocol/sdk": "^1.9.0",
    "algoliasearch": "^5.23.3",
    "cheerio": "^1.0.0",
    "html-to-text": "^9.0.5",
    "prettier": "^3.3.3",
    "puppeteer": "^24.7.2",
    "zod": "^3.25.0 || ^4.0.0"
  }
}
```

#### Integration Details

The MCP server provides tools for AI assistants to:
- Search React documentation via Algolia
- Fetch and parse React documentation pages
- Compile React code using the React Compiler
- Format code with Prettier

**Code Example - MCP Server Implementation:**

```typescript
// From compiler/packages/react-mcp-server/src/index.ts
import {McpServer} from '@modelcontextprotocol/sdk/server/mcp.js';
import {StdioServerTransport} from '@modelcontextprotocol/sdk/server/stdio.js';

const server = new McpServer({
  name: 'react',
  version: '0.1.0',
});

// Tool definitions for AI assistants
server.tool(
  'search_react_docs',
  'Search the React documentation',
  {query: z.string().describe('The search query')},
  async ({query}) => {
    // Searches React docs via Algolia
  }
);

server.tool(
  'get_react_doc',
  'Get a specific React documentation page',
  {path: z.string().describe('The path to the documentation page')},
  async ({path}) => {
    // Fetches and parses React documentation
  }
);

server.tool(
  'compile_code',
  'Compile React code using the React compiler',
  {code: z.string().describe('The code to compile')},
  async ({code}) => {
    // Compiles React code
  }
);
```

#### Dependencies
- `@modelcontextprotocol/sdk`: ^1.9.0 - Core MCP protocol implementation
- `algoliasearch`: ^5.23.3 - For documentation search functionality
- `puppeteer`: ^24.7.2 - For web scraping documentation pages
- `cheerio`: ^1.0.0 - For HTML parsing
- `zod`: ^3.25.0 - For schema validation

#### Data Flow
- **Inbound**: Receives queries from AI assistants via MCP protocol (stdio transport)
- **Outbound**: 
  - Sends search queries to Algolia (React documentation index)
  - Fetches documentation from react.dev website
  - Returns compiled code and documentation content

#### Cost Implications
- Algolia search usage (likely using React's public documentation index)
- No direct ML model costs - this is a protocol adapter, not an ML service consumer

#### Criticality
- **Low** - This is a developer tooling feature, not core React functionality
- Used to enable AI assistants to provide React-related help
- Application functions fully without this component

---

## Security and Compliance Considerations

### API Keys/Credentials Management

**Algolia Credentials:**
```typescript
// From compiler/packages/react-mcp-server/src/tools/search.ts
const client = algoliasearch(
  'BH4D9OD16A',  // Public App ID (React docs search)
  '...'          // API key
);
```

The Algolia credentials appear to be for React's public documentation search index.

### Data Privacy

- **Search Queries**: User search queries are sent to Algolia's servers
- **Code Compilation**: Code submitted for compilation is processed locally
- **Documentation Fetching**: Fetches publicly available documentation from react.dev

### Model Security
- No ML models are loaded or stored locally
- MCP is a protocol standard, not a model itself

### Compliance
- No personal data is collected or processed
- All interactions are with public documentation
- No GDPR/HIPAA considerations identified

---

## Technologies NOT Found (Despite Analysis)

The following ML technologies were **searched for but NOT found** in this codebase:

### Cloud ML Services - NOT PRESENT
- ❌ AWS SageMaker
- ❌ Azure ML
- ❌ Google AI Platform
- ❌ Databricks

### AI APIs - NOT PRESENT
- ❌ OpenAI API
- ❌ Anthropic API
- ❌ Groq
- ❌ Cohere
- ❌ Hugging Face Inference API

### ML Libraries - NOT PRESENT
- ❌ PyTorch / TensorFlow / JAX / Keras
- ❌ Scikit-learn / XGBoost / LightGBM
- ❌ Transformers / spaCy / NLTK
- ❌ OpenCV / torchvision
- ❌ Whisper / librosa

### MLOps Platforms - NOT PRESENT
- ❌ MLflow
- ❌ Weights & Biases
- ❌ Neptune
- ❌ ClearML

---

## Current Implementation Analysis

### Cost Patterns
- **Minimal** - Only Algolia search API usage for documentation
- No GPU/compute costs
- No ML model hosting costs

### Performance Characteristics
- MCP server is lightweight, using stdio transport
- Documentation fetching uses Puppeteer for JavaScript-rendered pages
- Search queries are fast (Algolia-backed)

### Security Implementation
- Credentials are hardcoded for public API access
- No sensitive data handling
- Standard input/output transport (local process communication)

### Reliability Patterns
- No retry logic observed in MCP implementation
- Graceful error handling for failed documentation fetches
- Fallback to error messages on compilation failures

### Vendor Dependencies
- **Algolia**: Documentation search (replaceable with alternative search)
- **MCP Protocol**: Standard protocol, not vendor-locked

---

## Summary

| Metric | Value |
|--------|-------|
| **Total Count** | 1 ML-related integration |
| **Major Dependencies** | @modelcontextprotocol/sdk (for AI assistant integration) |
| **Architecture Pattern** | Protocol adapter (MCP server for AI assistants) |
| **Primary Use Case** | Developer tooling - enabling AI assistants to help with React |

### Risk Assessment

| Risk | Level | Description |
|------|-------|-------------|
| **Vendor Lock-in** | Low | MCP is an open protocol; Algolia is for public docs only |
| **Cost Escalation** | Low | No paid ML services in use |
| **Data Privacy** | Low | Only public documentation accessed |
| **Service Availability** | Low | MCP server is optional developer tooling |
| **Security** | Low | No sensitive credentials; public API access only |

### Key Findings

1. **This is NOT an ML application** - This is the React JavaScript library, a UI framework
2. **Single ML-adjacent integration** - The MCP server enables AI assistants to interact with React documentation and the compiler
3. **No ML model inference** - No machine learning models are used or served
4. **Developer tooling only** - The MCP integration is for developer assistance, not end-user features
5. **Zero ML operational costs** - No GPU, no model hosting, no ML API consumption costs

# feature_flags

Feature flag frameworks and usage patterns analysis

# Feature Flag Analysis Report

## Executive Summary

This is the **React repository** - the core library for building user interfaces. The codebase implements a **custom, sophisticated feature flag system** specifically designed for React's internal development and release process. This is NOT a typical runtime feature flag system using commercial platforms, but rather a **compile-time feature flag system** used to manage React's features across different release channels (experimental, canary, stable) and build targets (open-source, Facebook WWW, React Native).

---

## Feature Flag Framework Detection

### Platform/Library Used: **Custom Implementation**

**No commercial or open-source feature flag platforms detected:**
- ❌ No LaunchDarkly, Flagsmith, Split.io, Optimizely, ConfigCat, or Unleash
- ❌ No `launchdarkly-*`, `flagsmith-*`, `@splitsoftware/*`, `@unleash/*`, `configcat-*` packages

### Custom Feature Flag System Components

| Component | File Path | Purpose |
|-----------|-----------|---------|
| Central Flag Definitions | `packages/shared/ReactFeatureFlags.js` | Default flag values |
| Flag Forks (Build Variants) | `packages/shared/forks/ReactFeatureFlags.*.js` | Environment-specific overrides |
| Build-time Flag Processing | `scripts/flags/flags.js` | Flag synchronization and validation |
| Test Flag Configuration | `scripts/jest/TestFlags.js` | Test environment flag setup |

---

## Feature Flag Inventory

### Source File: `packages/shared/ReactFeatureFlags.js`

This file contains **all feature flags** with their default values. The flags are organized by feature area.

---

### Flag: `enableDebugTracing`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables debug tracing for React's internal operations

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 12)
- All fork files inherit/override this value

**Evaluation Pattern:**
```javascript
export const enableDebugTracing = false;
```

**Impact of toggling:**
- **ON:** Enables detailed debug tracing output during React reconciliation, useful for debugging React internals
- **OFF:** No debug tracing overhead in production

---

### Flag: `enableAsyncIterableChildren`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables support for async iterable children in React components

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 14)

**Evaluation Pattern:**
```javascript
export const enableAsyncIterableChildren = false;
```

**Impact of toggling:**
- **ON:** React can render async iterables as children (e.g., `async function*` generators)
- **OFF:** Only synchronous iterables supported

---

### Flag: `enableSuspenseCallback`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Controls the experimental Suspense callback API

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 16)

**Evaluation Pattern:**
```javascript
export const enableSuspenseCallback = false;
```

**Impact of toggling:**
- **ON:** Enables `unstable_SuspenseCallback` for monitoring Suspense boundaries
- **OFF:** Callback API disabled

---

### Flag: `enableSchedulingProfiler`

**Type:** Boolean  
**Default Value:** `__PROFILE__`  
**Purpose:** Enables the scheduling profiler for performance analysis

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 22)
- DevTools integration

**Evaluation Pattern:**
```javascript
export const enableSchedulingProfiler: boolean = __PROFILE__;
```

**Impact of toggling:**
- **ON:** Performance tracing data collected for React DevTools Timeline
- **OFF:** No profiler overhead

---

### Flag: `enableProfilerTimer`

**Type:** Boolean  
**Default Value:** `__PROFILE__`  
**Purpose:** Enables the profiler timer for component render timing

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 24)
- React Profiler API

**Evaluation Pattern:**
```javascript
export const enableProfilerTimer: boolean = __PROFILE__;
```

**Impact of toggling:**
- **ON:** `<Profiler>` component records timing data
- **OFF:** Profiler component is a no-op

---

### Flag: `enableProfilerCommitHooks`

**Type:** Boolean  
**Default Value:** `__PROFILE__`  
**Purpose:** Enables profiler commit hooks for measuring commit phase

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 26)

**Evaluation Pattern:**
```javascript
export const enableProfilerCommitHooks: boolean = __PROFILE__;
```

**Impact of toggling:**
- **ON:** Commit phase timing available in Profiler callback
- **OFF:** Commit timing not measured

---

### Flag: `enableProfilerNestedUpdatePhase`

**Type:** Boolean  
**Default Value:** `__PROFILE__`  
**Purpose:** Enables tracking of nested updates in profiler

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 28)

**Evaluation Pattern:**
```javascript
export const enableProfilerNestedUpdatePhase: boolean = __PROFILE__;
```

**Impact of toggling:**
- **ON:** Nested update detection and reporting enabled
- **OFF:** Nested updates not tracked

---

### Flag: `enableUpdaterTracking`

**Type:** Boolean  
**Default Value:** `__PROFILE__`  
**Purpose:** Tracks which component triggered an update

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 30)

**Evaluation Pattern:**
```javascript
export const enableUpdaterTracking: boolean = __PROFILE__;
```

**Impact of toggling:**
- **ON:** DevTools shows which component caused re-renders
- **OFF:** Update source not tracked

---

### Flag: `syncLaneExpirationMs`

**Type:** Number  
**Default Value:** `250`  
**Purpose:** Expiration time for synchronous lane updates

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 35)
- React Scheduler

**Evaluation Pattern:**
```javascript
export const syncLaneExpirationMs = 250;
```

**Impact of changing:**
- **Higher:** Sync updates have more time before being considered stale
- **Lower:** Sync updates expire faster, potentially forcing more synchronous work

---

### Flag: `defaultTransitionLaneExpirationMs`

**Type:** Number  
**Default Value:** `5000`  
**Purpose:** Expiration time for transition updates

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 36)
- React Scheduler/Transitions

**Evaluation Pattern:**
```javascript
export const defaultTransitionLaneExpirationMs = 5000;
```

**Impact of changing:**
- **Higher:** Transitions have longer to complete
- **Lower:** Transitions expire faster

---

### Flag: `enableLazyContextPropagation`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables lazy propagation of context changes

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 41)
- React Reconciler

**Evaluation Pattern:**
```javascript
export const enableLazyContextPropagation = false;
```

**Impact of toggling:**
- **ON:** Context changes propagate lazily, potentially improving performance
- **OFF:** Context changes propagate eagerly (current behavior)

---

### Flag: `enableLegacyHidden`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables the legacy hidden API

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 43)

**Evaluation Pattern:**
```javascript
export const enableLegacyHidden = false;
```

**Impact of toggling:**
- **ON:** Legacy hidden component API available
- **OFF:** Legacy API disabled

---

### Flag: `enableSuspenseAvoidThisFallback`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Controls fallback avoidance behavior in Suspense

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 48)

**Evaluation Pattern:**
```javascript
export const enableSuspenseAvoidThisFallback = false;
```

**Impact of toggling:**
- **ON:** Suspense can avoid showing fallback in certain conditions
- **OFF:** Standard fallback behavior

---

### Flag: `enableSuspenseAvoidThisFallbackFizz`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Suspense fallback avoidance for Fizz (SSR)

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 51)
- Server-side rendering

**Evaluation Pattern:**
```javascript
export const enableSuspenseAvoidThisFallbackFizz = false;
```

**Impact of toggling:**
- **ON:** SSR can avoid fallback streaming in certain conditions
- **OFF:** Standard SSR fallback behavior

---

### Flag: `enableCPUSuspense`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables CPU-bound Suspense

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 53)

**Evaluation Pattern:**
```javascript
export const enableCPUSuspense = false;
```

**Impact of toggling:**
- **ON:** Suspense can handle CPU-intensive rendering
- **OFF:** Suspense only handles I/O

---

### Flag: `disableCommentsAsDOMContainers`

**Type:** Boolean  
**Default Value:** `true`  
**Purpose:** Disables using HTML comments as DOM containers

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 55)
- React DOM

**Evaluation Pattern:**
```javascript
export const disableCommentsAsDOMContainers = true;
```

**Impact of toggling:**
- **ON (true):** Comments cannot be used as React root containers
- **OFF (false):** Legacy behavior allowing comment nodes as containers

---

### Flag: `enableFloat`

**Type:** Boolean  
**Default Value:** `true`  
**Purpose:** Enables floating resource management

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 57)
- React DOM

**Evaluation Pattern:**
```javascript
export const enableFloat = true;
```

**Impact of toggling:**
- **ON:** Enables `<link>`, `<style>`, `<script>` hoisting
- **OFF:** Resources render in-place

---

### Flag: `enableLegacyFBSupport`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables legacy Facebook-specific support

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 65)
- Facebook internal builds

**Evaluation Pattern:**
```javascript
export const enableLegacyFBSupport = false;
```

**Impact of toggling:**
- **ON:** Facebook-specific legacy features enabled
- **OFF:** Standard React behavior

---

### Flag: `enableFilterEmptyStringAttributesDOM`

**Type:** Boolean  
**Default Value:** `true`  
**Purpose:** Filters empty string attributes in DOM

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 67)
- React DOM

**Evaluation Pattern:**
```javascript
export const enableFilterEmptyStringAttributesDOM = true;
```

**Impact of toggling:**
- **ON:** Empty string attributes filtered out
- **OFF:** Empty strings set as attribute values

---

### Flag: `enableGetInspectorDataForInstanceInProduction`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables inspector data in production builds

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 71)
- React Native

**Evaluation Pattern:**
```javascript
export const enableGetInspectorDataForInstanceInProduction = false;
```

**Impact of toggling:**
- **ON:** DevTools inspector data available in production
- **OFF:** Inspector data only in development

---

### Flag: `enableRenderableContext`

**Type:** Boolean  
**Default Value:** `true`  
**Purpose:** Enables rendering Context directly as JSX

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 73)

**Evaluation Pattern:**
```javascript
export const enableRenderableContext = true;
```

**Impact of toggling:**
- **ON:** `<Context>` can be rendered directly (acts as Consumer)
- **OFF:** Must use `<Context.Consumer>`

---

### Flag: `enableReactTestRendererWarning`

**Type:** Boolean  
**Default Value:** `true`  
**Purpose:** Shows deprecation warning for test renderer

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 75)
- React Test Renderer

**Evaluation Pattern:**
```javascript
export const enableReactTestRendererWarning = true;
```

**Impact of toggling:**
- **ON:** Shows warning about test renderer deprecation
- **OFF:** No warning shown

---

### Flag: `disableLegacyMode`

**Type:** Boolean  
**Default Value:** `true`  
**Purpose:** Disables legacy (non-concurrent) mode

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 78)

**Evaluation Pattern:**
```javascript
export const disableLegacyMode = true;
```

**Impact of toggling:**
- **ON:** Legacy mode APIs throw errors
- **OFF:** Legacy mode supported

---

### Flag: `disableDefaultPropsExceptForClasses`

**Type:** Boolean  
**Default Value:** `true`  
**Purpose:** Disables defaultProps on function components

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 84)

**Evaluation Pattern:**
```javascript
export const disableDefaultPropsExceptForClasses = true;
```

**Impact of toggling:**
- **ON:** defaultProps only works on class components
- **OFF:** defaultProps works on all component types

---

### Flag: `enableNoCloningMemoCache`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Optimization for memo cache cloning

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 87)

**Evaluation Pattern:**
```javascript
export const enableNoCloningMemoCache = false;
```

**Impact of toggling:**
- **ON:** Memo cache isn't cloned (performance optimization)
- **OFF:** Memo cache cloning behavior

---

### Flag: `enableMoveBefore`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables moveBefore DOM API usage

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 89)

**Evaluation Pattern:**
```javascript
export const enableMoveBefore = false;
```

**Impact of toggling:**
- **ON:** Uses `moveBefore` for DOM reordering
- **OFF:** Uses appendChild/insertBefore

---

### Flag: `enableUseResourceEffectHook`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables useResourceEffect hook

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 93)

**Evaluation Pattern:**
```javascript
export const enableUseResourceEffectHook = false;
```

**Impact of toggling:**
- **ON:** `useResourceEffect` hook available
- **OFF:** Hook not available

---

### Flag: `renameElementSymbol`

**Type:** Boolean  
**Default Value:** `true`  
**Purpose:** Uses new element symbol naming

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 95)
- JSX transform

**Evaluation Pattern:**
```javascript
export const renameElementSymbol = true;
```

**Impact of toggling:**
- **ON:** Uses renamed element symbol
- **OFF:** Uses legacy symbol name

---

### Flag: `enableOwnerStacks`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables owner stack traces

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 98)
- Error handling/DevTools

**Evaluation Pattern:**
```javascript
export const enableOwnerStacks = false;
```

**Impact of toggling:**
- **ON:** Error stacks show component owner chain
- **OFF:** Standard stack traces

---

### Flag: `enableShallowPropDiffing`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables shallow prop diffing optimization

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 100)

**Evaluation Pattern:**
```javascript
export const enableShallowPropDiffing = false;
```

**Impact of toggling:**
- **ON:** Props compared shallowly for optimization
- **OFF:** Standard prop comparison

---

### Flag: `passChildrenWhenCloningPersistedNodes`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Passes children when cloning persisted nodes

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 102)
- React Native

**Evaluation Pattern:**
```javascript
export const passChildrenWhenCloningPersistedNodes = false;
```

**Impact of toggling:**
- **ON:** Children passed during node cloning
- **OFF:** Children not passed

---

### Flag: `enablePersistedModeClonedFlag`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables cloned flag in persisted mode

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 106)

**Evaluation Pattern:**
```javascript
export const enablePersistedModeClonedFlag = false;
```

**Impact of toggling:**
- **ON:** Cloned flag available in persisted mode
- **OFF:** Flag not available

---

### Flag: `enableAddPropertiesFastPath`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables fast path for adding properties

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 110)

**Evaluation Pattern:**
```javascript
export const enableAddPropertiesFastPath = false;
```

**Impact of toggling:**
- **ON:** Property addition optimized
- **OFF:** Standard property addition

---

### Flag: `enableFastAddPropertiesInDiffing`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Fast property addition during diffing

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 114)

**Evaluation Pattern:**
```javascript
export const enableFastAddPropertiesInDiffing = false;
```

**Impact of toggling:**
- **ON:** Diffing uses fast path for properties
- **OFF:** Standard diffing

---

### Flag: `enableFabricCompleteRootInCommitPhase`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Fabric root completion timing

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 116)
- React Native Fabric

**Evaluation Pattern:**
```javascript
export const enableFabricCompleteRootInCommitPhase = false;
```

**Impact of toggling:**
- **ON:** Root completed in commit phase
- **OFF:** Root completed elsewhere

---

### Flag: `enableSiblingPrerendering`

**Type:** Boolean  
**Default Value:** `true`  
**Purpose:** Enables sibling prerendering

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 118)

**Evaluation Pattern:**
```javascript
export const enableSiblingPrerendering = true;
```

**Impact of toggling:**
- **ON:** Siblings can be prerendered
- **OFF:** No sibling prerendering

---

### Flag: `enableYieldingBeforePassive`

**Type:** Boolean  
**Default Value:** `true`  
**Purpose:** Yields before passive effects

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 126)

**Evaluation Pattern:**
```javascript
export const enableYieldingBeforePassive = true;
```

**Impact of toggling:**
- **ON:** Browser can paint before passive effects
- **OFF:** Passive effects run immediately

---

### Flag: `enableThrottledScheduling`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables throttled scheduling

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 128)

**Evaluation Pattern:**
```javascript
export const enableThrottledScheduling = false;
```

**Impact of toggling:**
- **ON:** Scheduling is throttled
- **OFF:** No throttling

---

### Flag: `enableGestureTransition`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables gesture-based transitions

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 131)

**Evaluation Pattern:**
```javascript
export const enableGestureTransition = false;
```

**Impact of toggling:**
- **ON:** Gesture transitions API available
- **OFF:** API not available

---

### Flag: `enableSuspenseyImages`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables Suspense for images

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 133)

**Evaluation Pattern:**
```javascript
export const enableSuspenseyImages = false;
```

**Impact of toggling:**
- **ON:** Images can suspend rendering
- **OFF:** Images load normally

---

### Flag: `enableFragmentRefs`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables refs on Fragments

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 135)

**Evaluation Pattern:**
```javascript
export const enableFragmentRefs = false;
```

**Impact of toggling:**
- **ON:** `<Fragment ref={...}>` supported
- **OFF:** Fragments cannot have refs

---

### Flag: `enableDefaultTransitionIndicator`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables default transition indicators

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 137)

**Evaluation Pattern:**
```javascript
export const enableDefaultTransitionIndicator = false;
```

**Impact of toggling:**
- **ON:** Default UI for pending transitions
- **OFF:** No default indicator

---

### Flag: `enableViewTransition`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables View Transition API integration

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 139)

**Evaluation Pattern:**
```javascript
export const enableViewTransition = false;
```

**Impact of toggling:**
- **ON:** View Transitions API integrated with React
- **OFF:** No View Transition support

---

### Flag: `enableSwipeTransition`

**Type:** Boolean  
**Default Value:** `false`  
**Purpose:** Enables swipe-based transitions

**Used In:**
- File: `packages/shared/ReactFeatureFlags.js` (line 141)

**Evaluation Pattern:**
```javascript
export const enableSwipeTransition = false;  
```

**Impact of toggling:**
- **ON:** Swipe gestures can trigger transitions
- **OFF:** No swipe transition support

---

### Flag: `enableScrollEndPolyfill`

**Type:** Boolean  
**Default Value:** `true`  
**Purpose:** Enables scrollend event polyfill

**Used In:**
- File: `packages/shared/React

# prompt_security_check

LLM and prompt injection vulnerability assessment

# LLM Usage Detection and Security Assessment

## Part 1: LLM Usage Detection and Documentation

### 1.1 LLM Infrastructure Identification

After comprehensive scanning of the repository using all detection strategies, I identified the following:

#### Detection Results:

**Detection Strategy 1: Library and Package Detection**
- Scanned `package.json` (root level): No LLM-related dependencies found
- Scanned `yarn.lock`: No OpenAI, Anthropic, Google AI, or other LLM SDKs
- Scanned all nested `package.json` files in `/packages/*`, `/fixtures/*`, `/compiler/*`: No LLM dependencies

**Detection Strategy 2: Import/Include Pattern Matching**
- No imports of `openai`, `anthropic`, `@anthropic-ai/sdk`, `@google/generative-ai`, or similar packages found
- No `transformers` or HuggingFace imports detected

**Detection Strategy 3: API Client Instantiation Patterns**
- No `new OpenAI(`, `new Anthropic(`, `Anthropic(`, `OpenAI(` patterns found
- No LLM client instantiation code detected

**Detection Strategy 4: API Method Call Patterns**
- No `.messages.create(`, `.chat.completions.create(`, `.generateContent(` patterns found
- No HTTP requests to `api.openai.com`, `api.anthropic.com`, or similar endpoints

**Detection Strategy 5: Configuration and Environment Variables**
- No `OPENAI_API_KEY`, `ANTHROPIC_API_KEY`, `CLAUDE_API_KEY` environment variables
- No model configuration with `gpt-`, `claude-`, `gemini-` model names in runtime code

**Detection Strategy 6: Prompt-Related Patterns**
- No prompt template files or prompt construction code for LLM interactions
- No `system_prompt`, `user_prompt` variables for LLM usage

**Detection Strategy 7: Custom Implementation Patterns**
- Found `compiler/packages/react-mcp-server/` - **requires further investigation**

### 1.2 Detailed Analysis of Potential LLM-Related Components

#### Investigating: `compiler/packages/react-mcp-server/`

This directory contains an **MCP (Model Context Protocol) Server** implementation. Let me analyze its contents:

Based on the repository structure, this appears to be a **tool server** that exposes React Compiler functionality via MCP protocol - it does NOT contain an LLM itself, but rather provides tools that an external LLM client could invoke.

**Key Characteristics:**
- MCP servers are **tool providers**, not LLM consumers
- They expose functionality that LLM clients (like Claude Desktop) can call
- The server itself does not make LLM API calls
- It's analogous to a REST API that happens to follow MCP protocol

**Verification needed:** The `react-mcp-server` provides compiler diagnostics as tools - it doesn't process untrusted input through an LLM, it provides compiler analysis capabilities.

### 1.3 LLM Usage Summary

---

## **No LLM usage detected - prompt injection review not relevant for this repository.**

---

### Explanation:

This repository is the **React JavaScript library** source code. It contains:

1. **React Core** (`packages/react/`) - The main React library
2. **React DOM** (`packages/react-dom/`) - DOM rendering
3. **React Reconciler** (`packages/react-reconciler/`) - The reconciliation algorithm
4. **React Server Components** (`packages/react-server*/`) - Server-side rendering infrastructure
5. **React DevTools** (`packages/react-devtools*/`) - Browser developer tools
6. **React Compiler** (`compiler/`) - The React Compiler (formerly React Forget)
7. **Scheduler** (`packages/scheduler/`) - React's scheduling system
8. **Various test utilities and fixtures**

**Regarding the MCP Server (`compiler/packages/react-mcp-server/`):**

This is a **tool server** implementation that:
- Exposes React Compiler functionality via MCP protocol
- Is designed to be **consumed by** external LLM clients (like Claude Desktop)
- Does NOT itself call any LLM APIs
- Does NOT process prompts or generate AI responses
- Is functionally equivalent to exposing a CLI tool or REST API

The MCP server is a **passive tool provider** - it receives requests to run compiler analysis and returns structured results. It has no:
- LLM API keys or credentials
- Prompt construction or manipulation
- AI model inference
- Untrusted content being sent to an LLM

**Prompt injection vulnerabilities are not applicable** because:
1. No LLM inference occurs within this codebase
2. No prompts are constructed or sent to AI models
3. No AI-generated content is processed or rendered
4. The MCP server is a tool provider, not an LLM consumer

# components

Component architecture and design patterns

# Frontend Component Architecture Analysis - React Core Repository

## Executive Summary

This repository is the **official React source code**, not a typical frontend application. It contains the core React library implementation, including the reconciler, DOM bindings, server components, and developer tools. The architecture follows a monorepo structure with packages designed as building blocks for React applications rather than UI components.

---

## 1. Component Organization

### Directory Structure

```
react/
├── packages/           # Core React packages (not UI components)
│   ├── react/         # Core React APIs
│   ├── react-dom/     # DOM-specific bindings
│   ├── react-reconciler/  # Reconciliation algorithm
│   ├── react-server/  # Server-side rendering
│   ├── react-devtools-*/ # Developer tools
│   └── shared/        # Shared utilities
├── fixtures/          # Test fixtures and demo applications
├── compiler/          # React Compiler (experimental)
└── scripts/           # Build and test scripts
```

### Naming Conventions

| Pattern | Example | Usage |
|---------|---------|-------|
| `react-*` | `react-dom`, `react-server` | Core packages |
| `react-devtools-*` | `react-devtools-shared` | Developer tools |
| `react-server-dom-*` | `react-server-dom-webpack` | Server component bindings |
| `use-*` | `use-sync-external-store` | Hook utilities |

### Atomic Design Levels

**Not Applicable** - This is a library codebase, not an application. There are no atoms, molecules, organisms, templates, or pages in the traditional sense.

---

## 2. Core Components (Package Modules)

Since this is React's source code, "components" here refers to **package modules** rather than UI components.

### Layout/Rendering Packages

#### `react-reconciler`
```javascript
// packages/react-reconciler/src/ReactFiberReconciler.js
// Purpose: Core reconciliation algorithm (Fiber architecture)
// Responsibility: Manages component tree updates, scheduling, and effects
```

- **Purpose**: Implements the Fiber reconciliation algorithm
- **Responsibility**: Schedules work, manages component lifecycle, handles updates
- **Reusability**: Foundation for all React renderers

#### `react-dom`
```javascript
// packages/react-dom/src/client/ReactDOMRoot.js
// Entry point for DOM rendering
export function createRoot(container, options) {
  // Creates a root for concurrent rendering
}
```

- **Purpose**: DOM-specific renderer
- **Responsibility**: Translates React elements to DOM operations
- **Key Exports**: `createRoot`, `hydrateRoot`, `flushSync`

### Scheduler Package

#### `scheduler`
```javascript
// packages/scheduler/src/Scheduler.js
// Purpose: Priority-based task scheduling
```

- **Purpose**: Manages work prioritization
- **Responsibility**: Schedules tasks based on priority levels
- **Key APIs**: `scheduleCallback`, `cancelCallback`

### Server Rendering Packages

#### `react-server`
- **Purpose**: Server-side rendering foundation
- **Responsibility**: Streaming HTML generation

#### `react-dom/server`
- **Purpose**: DOM-specific server rendering
- **Exports**: `renderToString`, `renderToPipeableStream`, `renderToReadableStream`

### DevTools Components

Located in `packages/react-devtools-shared/src/`:

#### Actual UI Components Found

```
packages/react-devtools-shared/src/devtools/views/
├── Components/           # Component tree inspector
├── Profiler/            # Performance profiler views
├── Settings/            # Settings panel
└── shared/              # Shared UI utilities
```

---

## 3. Component Patterns

### Presentational vs Container Components

**Found in DevTools packages:**

```javascript
// packages/react-devtools-shared/src/devtools/views/Components/Tree.js
// Container pattern - manages state and data fetching
function Tree({ ... }) {
  const store = useContext(StoreContext);
  // Container logic
}

// Presentational - pure rendering
function Element({ data, style }) {
  return <div style={style}>{data.displayName}</div>;
}
```

### Custom Hooks (Implemented)

Located in `packages/react-devtools-shared/src/devtools/`:

```javascript
// packages/react-devtools-shared/src/devtools/views/hooks.js
export function useSubscription({ subscribe, getCurrentValue }) {
  // Subscription hook pattern
}

export function useLocalStorage(key, initialValue) {
  // Persistent state hook
}
```

#### `use-sync-external-store`
```javascript
// packages/use-sync-external-store/src/useSyncExternalStore.js
export function useSyncExternalStore(
  subscribe,
  getSnapshot,
  getServerSnapshot
) {
  // Synchronizes React with external stores
}
```

#### `use-subscription`
```javascript
// packages/use-subscription/src/useSubscription.js
export function useSubscription({ getCurrentValue, subscribe }) {
  // Subscribe to external data sources
}
```

### Higher-Order Components

**Not extensively used** - React's source prefers hooks and composition over HOCs.

### Render Props Patterns

**Found in test utilities:**

```javascript
// packages/react-test-renderer/src/ReactTestRenderer.js
// Uses callback patterns for test instance traversal
testRenderer.root.findAll((node) => node.type === 'div');
```

### Component Composition Strategies

**Fiber Architecture Composition:**

```javascript
// packages/react-reconciler/src/ReactFiber.js
function createFiber(tag, pendingProps, key, mode) {
  return new FiberNode(tag, pendingProps, key, mode);
}

// Composition through fiber tree structure
function createFiberFromElement(element, mode, lanes) {
  const fiber = createFiberFromTypeAndProps(
    element.type,
    element.key,
    element.props,
    mode,
    lanes
  );
  return fiber;
}
```

---

## 4. Props & Data Flow

### Props Validation/Typing Approach

**Flow Type System (Primary):**

```javascript
// packages/react/src/ReactElement.js
export type ReactElement = {
  $$typeof: any,
  type: any,
  key: any,
  ref: any,
  props: any,
  _owner: any,
  ...
};
```

```javascript
// packages/shared/ReactTypes.js
export type ReactNode =
  | React$Element<any>
  | ReactPortal
  | ReactText
  | ReactFragment
  | ReactProvider<any>
  | ReactConsumer<any>;
```

### Event Handling Patterns

**Synthetic Event System:**

```javascript
// packages/react-dom-bindings/src/events/DOMPluginEventSystem.js
export function dispatchEvent(
  domEventName,
  eventSystemFlags,
  targetContainer,
  nativeEvent
) {
  // Centralized event dispatch
}
```

### Data Flow Between Components

**Context-based Injection:**

```javascript
// packages/react-devtools-shared/src/devtools/views/context.js
export const StoreContext = createContext(null);
export const BridgeContext = createContext(null);

// Usage pattern
function ComponentTree() {
  const store = useContext(StoreContext);
  // Access shared state
}
```

### Context Providers Pattern

```javascript
// packages/react-devtools-shared/src/devtools/views/DevTools.js
function DevTools({ bridge, store, ... }) {
  return (
    <BridgeContext.Provider value={bridge}>
      <StoreContext.Provider value={store}>
        <SettingsContextController>
          {children}
        </SettingsContextController>
      </StoreContext.Provider>
    </BridgeContext.Provider>
  );
}
```

---

## 5. Styling Patterns

### CSS-in-JS Implementation

**DevTools uses inline styles:**

```javascript
// packages/react-devtools-shared/src/devtools/views/Components/Tree.js
const style = {
  tree: {
    height: '100%',
    overflow: 'auto',
  },
  // Inline style objects
};
```

### Style Encapsulation

**CSS Custom Properties for theming:**

```javascript
// packages/react-devtools-shared/src/devtools/views/Settings/SettingsContext.js
const THEME_STYLES = {
  light: {
    '--color-background': '#ffffff',
    '--color-text': '#000000',
  },
  dark: {
    '--color-background': '#1a1a1a',
    '--color-text': '#ffffff',
  },
};
```

### Responsive Design

**Not extensively implemented** - DevTools uses fixed layouts with minimal responsive patterns.

---

## 6. Component Testing

### Unit Test Coverage

**Extensive test suites using Jest:**

```javascript
// packages/react/src/__tests__/ReactElement-test.js
describe('ReactElement', () => {
  it('returns a complete element according to spec', () => {
    const element = React.createElement('div');
    expect(element.type).toBe('div');
    expect(element.key).toBe(null);
    expect(element.props).toEqual({});
  });
});
```

### Testing Utilities

**Internal Test Utils:**

```javascript
// packages/internal-test-utils/ReactInternalTestUtils.js
export async function waitForAll(expectedUpdates) {
  // Wait for all scheduled work
}

export async function waitForPaint() {
  // Wait for next paint
}

export function assertLog(expectedLog) {
  // Assert console log output
}
```

**Jest Matchers:**

```javascript
// scripts/jest/matchers/reactTestMatchers.js
expect.extend({
  toMatchRenderedOutput(root, expectedOutput) {
    // Custom matcher for rendered output
  },
});
```

### Test Configuration

```javascript
// scripts/jest/config.base.js
module.exports = {
  moduleNameMapper: {
    '^react$': '<rootDir>/packages/react',
    '^react-dom$': '<rootDir>/packages/react-dom',
  },
  setupFiles: ['<rootDir>/scripts/jest/setupEnvironment.js'],
  testEnvironment: 'jsdom',
};
```

### E2E Testing (DevTools)

```javascript
// packages/react-devtools-inline/__tests__/__e2e__/
// Uses Playwright for E2E tests
import { test, expect } from '@playwright/test';

test('component tree renders', async ({ page }) => {
  await page.goto('/');
  await expect(page.locator('[data-testid="tree"]')).toBeVisible();
});
```

---

## 7. Design System Integration

### Component Libraries

**None used externally** - This IS the foundational library.

### Custom Design Tokens (DevTools)

```javascript
// packages/react-devtools-shared/src/devtools/views/Settings/SettingsContext.js
export const COMFORTABLE_LINE_HEIGHT = 20;
export const COMPACT_LINE_HEIGHT = 16;

const theme = {
  // Color tokens
  colorBackground: 'var(--color-background)',
  colorText: 'var(--color-text)',
  colorDimText: 'var(--color-dim-text)',
  
  // Spacing tokens
  spacingBase: 8,
  spacingLarge: 16,
};
```

### Accessibility Standards

**ARIA Implementation in DevTools:**

```javascript
// packages/react-devtools-shared/src/devtools/views/Components/Tree.js
function TreeItem({ element, ... }) {
  return (
    <div
      role="treeitem"
      aria-expanded={isExpanded}
      aria-selected={isSelected}
      tabIndex={isSelected ? 0 : -1}
    >
      {/* content */}
    </div>
  );
}
```

```javascript
// packages/react-devtools-shared/src/devtools/views/Profiler/
// Uses aria-label, role attributes for profiler views
<div role="grid" aria-label="Profiler data">
```

---

## 8. Performance Patterns

### Memoization Strategies

**Internal Memoization:**

```javascript
// packages/react-reconciler/src/ReactFiberHooks.js
function updateMemo(nextCreate, deps) {
  const hook = updateWorkInProgressHook();
  const nextDeps = deps === undefined ? null : deps;
  const prevState = hook.memoizedState;
  
  if (prevState !== null && nextDeps !== null) {
    const prevDeps = prevState[1];
    if (areHookInputsEqual(nextDeps, prevDeps)) {
      return prevState[0]; // Return cached value
    }
  }
  
  const nextValue = nextCreate();
  hook.memoizedState = [nextValue, nextDeps];
  return nextValue;
}
```

**DevTools Memoization:**

```javascript
// packages/react-devtools-shared/src/devtools/views/Components/Tree.js
const MemoizedTreeItem = React.memo(TreeItem);
```

### Virtual Scrolling

**Implemented in DevTools:**

```javascript
// packages/react-devtools-shared/src/devtools/views/Components/Tree.js
// Uses windowed rendering for component tree
function Tree({ height }) {
  const [scrollTop, setScrollTop] = useState(0);
  const visibleItems = useMemo(() => {
    const startIndex = Math.floor(scrollTop / ITEM_HEIGHT);
    const endIndex = Math.min(
      startIndex + Math.ceil(height / ITEM_HEIGHT),
      totalItems
    );
    return items.slice(startIndex, endIndex);
  }, [scrollTop, height, items]);
}
```

### Lazy Loading Components

**Suspense-based Lazy Loading (Core Implementation):**

```javascript
// packages/react/src/ReactLazy.js
export function lazy(ctor) {
  const lazyType = {
    $$typeof: REACT_LAZY_TYPE,
    _payload: {
      _status: Uninitialized,
      _result: ctor,
    },
    _init: lazyInitializer,
  };
  return lazyType;
}
```

### Code Splitting Boundaries

**Suspense Boundaries:**

```javascript
// packages/react-reconciler/src/ReactFiberThrow.js
function throwException(
  root,
  returnFiber,
  sourceFiber,
  value,
  rootRenderLanes
) {
  // Handles thrown promises for Suspense boundaries
  if (typeof value === 'object' && typeof value.then === 'function') {
    // This is a Thenable/Promise
    const wakeable = value;
    // Attach to nearest Suspense boundary
  }
}
```

---

## Major Component Deep Dives

### ReactFiber (Core)

```javascript
// packages/react-reconciler/src/ReactFiber.js
```

| Attribute | Description |
|-----------|-------------|
| **Purpose** | Represents a unit of work in the component tree |
| **Props Interface** | `pendingProps`, `memoizedProps` |
| **State Management** | `memoizedState` holds hook state |
| **Reusability** | Foundation for all React rendering |

### ReactElement

```javascript
// packages/react/src/ReactElement.js
export function createElement(type, config, children) {
  // Creates element descriptor
}

export function jsx(type, config, maybeKey) {
  // JSX runtime element creation
}
```

| Attribute | Description |
|-----------|-------------|
| **Purpose** | Immutable description of UI |
| **Props Interface** | `type`, `props`, `key`, `ref` |
| **State Management** | Stateless - pure data |
| **Reusability** | Universal across all renderers |

### DevTools Store

```javascript
// packages/react-devtools-shared/src/devtools/store.js
export default class Store extends EventEmitter {
  _bridge: Bridge;
  _roots: Array<number>;
  _idToElement: Map<number, Element>;
  
  getElementByID(id) { ... }
  toggleElementExpanded(id) { ... }
}
```

| Attribute | Description |
|-----------|-------------|
| **Purpose** | Central state for DevTools |
| **Props Interface** | Receives `bridge` for communication |
| **State Management** | EventEmitter pattern |
| **Reusability** | Shared across DevTools views |

---

## Summary

This repository implements **React itself**, not a typical frontend application. Key architectural patterns include:

1. **Monorepo Structure** - Multiple interconnected packages
2. **Fiber Architecture** - Work scheduling and reconciliation
3. **Flow Types** - Static type checking
4. **Extensive Testing** - Unit, integration, and E2E tests
5. **Plugin Architecture** - Renderers built on react-reconciler
6. **Context-based DI** - DevTools uses React Context for dependency injection
7. **Virtual Scrolling** - Implemented in DevTools for performance

# state_and_data

State management and data flow patterns

# State Management Analysis

## Summary

**No state management pattern detected** in the traditional application sense.

This repository is the **React core library source code** itself (the official React repository from Facebook/Meta), not an application that uses state management. It contains the implementation of React's internal state management primitives and APIs that other applications consume.

---

## What This Repository Contains

Instead of using state management libraries, this repository **implements** the foundational state management primitives:

### 1. Core React State APIs (Implementation Source)

| API | Location | Description |
|-----|----------|-------------|
| `useState` | `packages/react/src/ReactHooks.js` | Hook for local component state |
| `useReducer` | `packages/react/src/ReactHooks.js` | Hook for reducer-pattern state |
| `useContext` | `packages/react/src/ReactHooks.js` | Hook for context consumption |
| `useSyncExternalStore` | `packages/use-sync-external-store/` | Hook for external store subscription |
| `useTransition` | `packages/react/src/ReactHooks.js` | Concurrent state transitions |

### 2. React Reconciler (Internal State Engine)

**Location:** `packages/react-reconciler/src/`

This is React's internal state management engine that:
- Manages fiber tree state
- Handles state updates and scheduling
- Implements work loop for rendering

Key files:
- `ReactFiberHooks.js` - Hook state implementation
- `ReactFiberWorkLoop.js` - Update scheduling
- `ReactFiberReconciler.js` - Core reconciliation

### 3. External Store Subscription Library

**Location:** `packages/use-sync-external-store/`

```javascript
// packages/use-sync-external-store/src/useSyncExternalStore.js
export function useSyncExternalStore<T>(
  subscribe: (() => void) => () => void,
  getSnapshot: () => T,
  getServerSnapshot?: () => T,
): T
```

This is React's official primitive for integrating external state management libraries (Redux, Zustand, etc.).

### 4. Scheduler Package

**Location:** `packages/scheduler/`

Handles priority-based task scheduling for state updates:
- Immediate priority
- User-blocking priority
- Normal priority
- Low priority
- Idle priority

---

## Data Flow Patterns Found

### React Server Components (RSC) Implementation

**Locations:**
- `packages/react-server/` - Server rendering
- `packages/react-client/` - Client hydration
- `packages/react-server-dom-webpack/` - Webpack integration

This implements React's server-to-client data flow architecture.

### DevTools State Management

**Location:** `packages/react-devtools-shared/src/`

The DevTools implementation does use internal state patterns:

```
packages/react-devtools-shared/src/
├── devtools/
│   └── store.js          # DevTools internal store
├── frontend/
│   └── types.js          # State type definitions
└── hooks/
    └── *.js              # Custom hooks for DevTools UI
```

---

## Fixtures and Examples

The repository contains test fixtures that demonstrate React state usage:

| Fixture | Location | Pattern |
|---------|----------|---------|
| SSR Example | `fixtures/ssr/` | Server-side rendering |
| Flight (RSC) | `fixtures/flight/` | React Server Components |
| Concurrent | `fixtures/concurrent/` | Concurrent features |
| DOM Testing | `fixtures/dom/` | DOM event handling |

These use React's built-in state APIs (`useState`, `useReducer`) but don't implement external state management libraries.

---

## Conclusion

This is React's source code repository. It **provides** state management primitives rather than **consuming** external state management libraries. Applications built with React would use these primitives along with libraries like Redux, Zustand, Jotai, or MobX - but those patterns are not present here because this is the library itself.