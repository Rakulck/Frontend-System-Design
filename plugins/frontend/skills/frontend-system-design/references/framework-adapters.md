# Framework Adapters

Use this file for framework-aware execution. Analysis is universal; execution must match the detected stack.

## React / Vite / SPA

Look for: `package.json`, `vite.config.*`, `src/main.*`, `src/App.*`, `components/`, `hooks/`, `services/`, `api/`, `store/`.

Safe patterns:

- Keep API logic in existing services/hooks when present.
- Add loading/error/empty states around data screens.
- Use existing query/cache/state tools if present.
- Add debounce/cancellation for search and rapid input.
- Avoid global state for local UI state.

## Next.js

Detect App Router vs Pages Router.

App Router signals: `app/`, `src/app`, `layout.tsx`, `page.tsx`, `loading.tsx`, `error.tsx`.
Pages Router signals: `pages/`, `getServerSideProps`, `getStaticProps`, `api/` routes.

Safe patterns:

- Avoid unnecessary client components.
- Use `loading.tsx` and `error.tsx` when route-level states fit.
- Respect server/client boundaries.
- Do not move auth-sensitive logic client-side.
- Use existing fetch/cache/server-action patterns.

## React Native / Expo

Look for: `app.json`, `app.config.*`, `expo`, `android/`, `ios/`, `screens/`, navigation files.

Account for:

- Slow network
- Offline state
- App backgrounding
- Upload progress/retry/cancel
- SecureStore vs AsyncStorage
- Navigation state
- Mobile performance

Safe patterns:

- Add non-blocking loading and error states.
- Persist safe last-known-good data when the app already has storage patterns.
- Avoid storing sensitive tokens in AsyncStorage.
- Handle upload retries carefully.

## Flutter

Look for: `pubspec.yaml`, `lib/`, `android/`, `ios/`.

Respect existing state management: Provider, Riverpod, Bloc, GetX, setState, etc.

Safe patterns:

- Separate service/repository logic from widgets when it is clearly mixed.
- Add loading/error/empty states around Future/Stream flows.
- Do not migrate state management unless asked.
- Use existing folder conventions.

## Vue / Nuxt

Look for: `vue`, `nuxt`, `pages/`, `composables/`, `stores/`, `components/`.

Safe patterns:

- Use existing composables/services for API logic.
- Add loading/error states around async data.
- Respect Pinia/Vuex if present.
- Avoid global state for local UI state.

## Angular

Look for: `angular.json`, `src/app`, modules, services, guards, interceptors.

Safe patterns:

- Move transport logic into services when components directly own it.
- Use guards for route-level auth checks when project patterns support it.
- Use interceptors for shared auth/error behavior only when justified.
- Respect RxJS patterns already present.

## Svelte / SvelteKit

Look for: `svelte.config.*`, `src/routes`, `+page.*`, `+layout.*`, `load` functions.

Safe patterns:

- Respect route load functions and stores.
- Add error/loading states without forcing unrelated architecture.
- Keep server-only data server-side.

## Blazor / ASP.NET MVC / Razor

Look for: `*.csproj`, `Program.cs`, `Pages/`, `Views/`, `Components/`, `.razor` files.

Clarify type:

- Blazor: components, services, state containers, auth handling.
- Razor/MVC: views, partials, forms, validation, JS interop.
- Backend API only: analyze frontend/API contract boundary instead of pretending it is a frontend app.

Safe patterns:

- Improve component/view loading and validation states.
- Avoid backend contract changes unless asked.
- Respect server-rendered flow.
