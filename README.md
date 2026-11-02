# DocPlan Executor

Interactive execution, task breakdown, and progress tracking dashboard for Google Docs plans.

## Overview

DocPlan Executor turns static Google Docs plan documents into an interactive engineering execution workspace. It signs in to Google with client-side OAuth, reads a Google Doc (read-only), parses its structure into deliverables and milestones, and can export reports to Google Drive. The sync is one-way: your task changes are never written back to the source document.

## Features

- **Google Workspace OAuth Integration**: Client-side sign-in with Firebase Auth and the Google Identity Services token client. Access tokens are kept in memory only. Without a token the app runs in a demo mode on a built-in sample plan.
- **Intelligent Google Docs Parser**: Automatically extracts headings, paragraphs, bullet points, checklists, tables, and the revision ID into actionable plan items.
- **Interactive Kanban Execution Board**: 4-stage workflow (*To Do*, *In Progress*, *In Review*, *Done*) with subtask checklists, stage advances, and direct completion checkboxes.
- **Phased Milestone Roadmap**: Phased progress bars, target dates, and direct deliverable check-off controls.
- **Full Plan Document Reader**: In-document keyword search, dynamic Table of Contents, table viewer, and one-click "+ Turn into Task" extraction.
- **Executive Analytics & Reporting**: Real-time progress metrics, priority risk breakdown, and multi-format exports:
  - **Export to Google Docs Folder**: Automatically creates a dedicated Google Drive folder with 4 formatted Google Docs (Executive Status Brief, Deliverables Matrix, Roadmap Specification, Plan Archive).
  - **Markdown Status Report** (`.md`)
  - **Structured Plan Data** (`.json`)
  - **Tasks Spreadsheet** (`.csv`) for Google Sheets and Excel
  - **Print / Save as PDF Executive Brief**

## Tech Stack

- **Frontend**: React 19, TypeScript, Tailwind CSS, Vite
- **Icons**: Lucide React
- **Authentication**: Firebase Authentication + Google Identity Services (GIS)
- **APIs**: Google Docs API v1, Google Drive API v3

## Getting Started

### Installation

```bash
npm install
```

### Development Server

```bash
npm run dev
```

Runs the development server on `http://localhost:3000` (it listens on all network interfaces).

### Production Build and type check

```bash
npm run build     # production bundle
npm run lint      # TypeScript type check (tsc --noEmit); there is no unit test suite
```

`.env.example` lists `GEMINI_API_KEY` and `APP_URL`, which come from the AI Studio template this app started from. Nothing in `src/` uses the Gemini API. Google sign-in uses the Firebase settings in `firebase-applet-config.json`.

## Security & Privacy

- **Local task state**: your task edits are saved in the browser's `localStorage` (tasks only, never tokens), so they stay on one browser and are not synced anywhere.
- **In-Memory Token Lifecycle**: OAuth access tokens are stored strictly in memory and cleared on sign-out or session end. Tokens are never persisted to localStorage or sessionStorage.
- **User Confirmation**: All write operations to Google Drive (folder creation and Google Docs export) require explicit user confirmation before executing.

## Licence

Apache License 2.0. See [LICENSE](LICENSE).
