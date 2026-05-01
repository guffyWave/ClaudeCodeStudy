# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev      # Start development server at http://localhost:5173
npm run build    # Production build via Vite
npm run preview  # Preview production build locally
npm run lint     # Run ESLint
```

No test runner is configured.

## Architecture

Single-page React app (React 19 + Vite) for tracking personal income and expenses. All application logic lives in one component: `src/App.jsx`.

**State:** Local `useState` hooks manage the transactions array, form inputs, and active filters.

**Data flow:**
1. User fills out the add-transaction form → state update appends to transactions array
2. Filter controls (type/category) recalculate a filtered view of transactions
3. Summary cards (income total, expense total, balance) are derived values computed from the transactions array

There is no backend, no routing, and no persistent storage — everything resets on page reload.

## Key context

This project is intentionally built with bugs, poor UI, and messy code as a learning exercise. Improvements — refactoring, bug fixes, component extraction — are the expected work here.

Known bugs in the current code:
- `amount` is stored as a string (input value is never parsed), so the `reduce` calls in the summary totals use string concatenation instead of addition — totals are wrong.
- The seed transaction "Freelance Work" (id 4) is typed `"expense"` but categorized as `"salary"` — it should be `"income"`.
