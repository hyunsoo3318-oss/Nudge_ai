# Nudge AI

> _A smart AI that calls children on a parent's behalf to teach financial sense and good daily habits — one gentle conversation at a time._

![React](https://img.shields.io/badge/React-19-61DAFB?style=flat&logo=react&logoColor=black)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Create React App](https://img.shields.io/badge/Create%20React%20App-09D3AC?style=flat&logo=createreactapp&logoColor=white)

## Overview

**Nudge AI** is a React single-page application that demonstrates a children's allowance and habit-coaching product built around AI-mediated phone calls. From a single login, the app branches into two fully distinct experiences — a **child app** for spending, missions, and savings, and a **parent dashboard** for payment approvals, AI rule-teaching, and call-log review. The flagship interaction is a scripted, real-time AI call simulation that intercepts a payment, talks the child through the decision against the family's rules, and surfaces the resulting transcript and recommendation to the parent.

## Technical Highlights

- **Selection-screen routing into two sub-apps** — after login the app lands on a `SelectionScreen` that uses `useNavigate` to branch into entirely separate parent and child experiences, each implemented as its own self-contained component (`ChildApp`, `ParentApp`) with its own navigation, screens, and visual theme.
- **Flat React Router structure** — `App.js` defines four `BrowserRouter` routes: `/` (login), `/select` (mode selection), `/child`, and `/parent`, with each sub-app providing a "back" control that routes the user back to `/select`.
- **Login / signup with role selection** — `LoginScreen` toggles between login and signup forms in local state, performs inline validation (required fields, password match, minimum length), persists session info to `localStorage`, supports a parent/child role choice on signup, and offers a no-login "demo mode" that jumps straight to `/select`.
- **Scripted real-time AI call flow** — the child app models call state as `none → incoming → incall`. A payment attempt (QR scan or simple-pay) triggers an incoming call screen; answering opens a live chat view where a sequence of `setTimeout` timers reveals AI and child messages in turn, complete with a running call-duration timer, mute toggle, and a typing indicator that appears between turns.
- **Auto-scrolling chat transcript** — the in-call message list is held in `useState` and auto-scrolls to the newest message via a `useRef` on the container with smooth `scrollTo` behavior on every update.
- **Multi-state payment flow** — the child payment screen drives a `paymentStatus` machine (`none`, `qr`, `manual`, `waiting`, …) covering payment-method selection, a simulated QR scanner, an online simple-pay detection view with pending/approved/rejected history, and an "AI is checking" waiting state — all wired to launch the AI call.
- **Parent dashboard with call-log drill-down** — `ParentApp` renders AI call logs (payment vs. mission calls) that open a modal showing the full timestamped conversation, plus pending-approval cards carrying the AI's recommendation and reason, recent-payment history with approve/reject actions, and savings/spending summary cards.
- **Conversational AI rule-teaching** — parents add payment rules in natural language; a guided dialog then asks follow-up questions (category, time window, weekend applicability) through a branching `setTimeout`-driven message flow before committing the new rule into state, mirroring how an AI would clarify intent.
- **Distinct theming per role** — the child app uses a light, rounded, gamified UI (levels, points, badges, progress bars) while the parent dashboard adopts a dark `stone-` palette, making the two modes visually unmistakable.

## Tech Stack

- **React 19** — component-based UI with hooks (`useState`, `useEffect`, `useRef`)
- **React Router (`react-router-dom` 7)** — client-side routing across login, selection, and the two sub-apps
- **Tailwind CSS 3** — utility-first styling, configured via PostCSS/Autoprefixer
- **lucide-react** — icon set used throughout both apps
- **Create React App (`react-scripts`)** — development server, build tooling, and test runner

## Getting Started

Install dependencies and run the development server:

```bash
npm install
npm start
```

From the login screen you can sign up, log in, or tap **demo mode** to explore both apps without credentials.

Other available scripts (from `package.json`):

```bash
npm run build   # production build into build/
npm test        # run the test runner
```
