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

Single-page React app (React 19 + Vite) for tracking personal income and expenses.

**Component tree:**
- `App` — holds the `transactions` array in state and passes it down; the only component that calls `setTransactions`
  - `Summary` — receives `transactions`, computes `totalIncome`, `totalExpenses`, and `balance` internally
  - `AddTransaction` — owns its own form state; calls `onAdd(transaction)` prop to append to the array
  - `TransactionList` — receives `transactions`, owns filter state (type/category) internally

**Data flow:**
1. User submits the form in `AddTransaction` → `onAdd` fires → `App` appends to `transactions`
2. `Summary` and `TransactionList` re-render with the updated array
3. Filter controls inside `TransactionList` derive a filtered view locally without lifting state

There is no backend, no routing, and no persistent storage — everything resets on page reload.

## Key context

This project is intentionally built with bugs, poor UI, and messy code as a learning exercise. Improvements — refactoring, bug fixes, component extraction — are the expected work here.

Known bugs fixed:
- `amount` was stored as a string; now parsed to `Number` in `AddTransaction` on submit and stored as numeric literals in seed data
- The seed transaction "Freelance Work" (id 4) is typed `"expense"` but categorized as `"salary"` — it should be `"income"` (not yet fixed)
