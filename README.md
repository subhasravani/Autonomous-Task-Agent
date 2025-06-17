# Autonomous Task Agent


## Overview
Autonomous Task Agent is a full-stack application that combines a modern Next.js frontend with a backend canister running on the Internet Computer (ICP). This project sets up the foundational infrastructure for developing an autonomous agent, leveraging decentralized technology for its operations.

## Tech Stack

*   **Frontend:**
    *   [Next.js](https://nextjs.org/) (v15) - React framework for building user interfaces.
    *   [React](https://reactjs.org/) (v19) - JavaScript library for building user interfaces.
    *   [TypeScript](https://www.typescriptlang.org/) - Typed superset of JavaScript.
    *   [Tailwind CSS](https://tailwindcss.com/) - Utility-first CSS framework.
    *   [Shadcn UI](https://ui.shadcn.com/) - Re-usable UI components, configured with Lucide icons.
*   **Backend:**
    *   [Internet Computer (ICP)](https://internetcomputer.org/) - A decentralized cloud platform.
    *   [Motoko](https://internetcomputer.org/docs/current/motoko/main/motoko) - A programming language designed for ICP canisters.
*   **Package Manager:**
    *   [pnpm](https://pnpm.io/)

## Project Structure

The repository is structured with a Next.js frontend and an ICP backend canister:

*   **Backend (ICP Canister):**
    *   Canister Name: `autonomous_task_agent`
    *   The main Motoko source file is configured in `dfx.json` as `src/autonomous_task_agent/main.mo`.
    *   The provided `main.mo` file (currently located at the project root) contains a simple actor with a `greet` function:
        ```motoko
        actor autonomous_task_agent {
          public func greet() : async Text {
            "Hello, ICP!"
          };
        };
        ```
    *   **Note:** For `dfx` to build the canister correctly, ensure the `main.mo` file is located at `src/autonomous_task_agent/main.mo`, or update the path in `dfx.json`.

*   **Frontend (Next.js Application):**
    *   A Next.js 15 project likely utilizing the App Router (indicated by `rsc: true` in `components.json` and Tailwind CSS configuration looking for files in `app/`).
    *   Configured with TypeScript, Tailwind CSS, and Shadcn UI.
    *   Key frontend configuration files include: `next.config.mjs`, `tailwind.config.ts`, `components.json`, `tsconfig.json`, and `package.json`.

## Getting Started

### Prerequisites

*   [Node.js](https://nodejs.org/) (compatible with Next.js 15 and React 19, typically latest LTS)
*   [pnpm](https://pnpm.io/installation)
*   [DFINITY Canister SDK (dfx)](https://internetcomputer.org/docs/current/developer-docs/setup/install/) (version `0.27.0` or compatible, as specified in `dfx.json`)

### Backend Setup (ICP Canister)

1.  **Start the local replica (if not already running):**
    ```bash
    dfx start --background
    ```
    This command is for local development. For deploying to the IC mainnet, this step is not needed.

2.  **Deploy the canister:**
    *   For local deployment:
        ```bash
        dfx deploy autonomous_task_agent
        ```
    *   For IC mainnet deployment (ensure you have cycles):
        ```bash
        dfx deploy --network ic autonomous_task_agent
        ```

### Frontend Setup

1.  **Navigate to the project root directory.**

2.  **Install dependencies:**
    ```bash
    pnpm install
    ```

3.  **Run the development server:**
    ```bash
    pnpm dev
    ```
    The application will typically be available at `http://localhost:3000` (or the port specified by Next.js).

## Configuration

Key configuration files in this project:

*   **`dfx.json`**: Configures the ICP canister(s).
    *   Defines the `autonomous_task_agent` canister, its type (`motoko`), and the entry point for its source code (`src/autonomous_task_agent/main.mo`).
    *   Specifies DFX version (`0.27.0`) and network configurations for `local` and `ic` environments.

*   **`package.json`**: Manages frontend project metadata, dependencies, and scripts.
    *   Lists numerous `@radix-ui/*` components, `lucide-react` for icons, `react-hook-form` for forms, `zod` for validation, `next-themes`, and other UI/utility libraries.
    *   Defines scripts for development (`dev`), building (`build`), starting (`start`), and linting (`lint`).

*   **`next.config.mjs`**: Next.js specific configurations.
    *   Currently configured to ignore ESLint and TypeScript errors during builds, and sets images to be unoptimized.

*   **`tailwind.config.ts`**: Tailwind CSS configuration.
    *   Enables dark mode (`class` strategy).
    *   Specifies content paths covering `pages`, `components`, and `app` directories.
    *   Defines custom theme properties (colors, border radius) and animations (`accordion-down`, `accordion-up`) using `tailwindcss-animate` plugin.

*   **`components.json`**: Shadcn UI configuration.
    *   Specifies UI style (`default`), RSC compatibility (`true`), TypeScript usage (`true`).
    *   Defines Tailwind CSS settings (config file, CSS file path `app/globals.css`, base color).
    *   Sets up path aliases (`@/components`, `@/lib/utils`, etc.) for streamlined imports.
    *   Uses `lucide` as the icon library.

*   **`tsconfig.json`**: TypeScript compiler options for the Next.js frontend.
    *   Configured for modern JavaScript (ESNext module, ES6 target), JSX preservation, strict type checking, and path aliases resolution (`@/*`).

## Available Scripts (Frontend)

The following scripts are available via `pnpm` for the frontend application:

*   `pnpm dev`: Starts the Next.js development server with hot reloading.
*   `pnpm build`: Compiles the Next.js application for production.
*   `pnpm start`: Runs the production build of the Next.js application.
*   `pnpm lint`: Runs ESLint to check for code quality and style issues.
