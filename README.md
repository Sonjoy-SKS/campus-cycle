# 🚲 CampusCycle

A campus bike-share demo built for **IDP-2**. Students unlock a cycle from any dock on
campus and pay **৳100/hour** (billed per minute) using **bKash, Rocket, Nagad, or Upay**.

**Live demo:** _add your Vercel URL here after deploying_

---

## What it does

- **Wallet (metro-card style balance)** — top up your CampusCycle balance using
  bKash / Rocket / Nagad / Upay. Once funded, unlocking a cycle deducts straight from the
  balance — no repeat gateway payment for every ride, just like tapping a metro card.
- **Dock Board** — live view of 6 campus docks with cycle availability, search + filter
- **Booking flow** — pick a duration (30 min / 1 hr / 2 hr / 3 hr), fare is calculated live
- **Smart balance check** — if your wallet has enough, you confirm and unlock instantly;
  if it doesn't, you're routed straight into a top-up (pre-filled with the exact shortfall)
  and the ride unlocks automatically the moment the top-up succeeds
- **Payment gateway (simulated)** — used only for topping up the wallet: choose bKash /
  Rocket / Nagad / Upay, enter a wallet number + PIN, watch a realistic "confirming with
  your wallet" loading state
- **Digital ride ticket** — on success you get an unlock code + receipt (station, duration,
  amount, "Paid via Wallet Balance")
- **My Rides** — history of active/completed rides, with an "End ride" action
- **Transaction history** — every top-up and ride deduction, newest first
- **Campus Impact** — live stats: rides completed, money topped up via mobile wallets,
  minutes ridden, and an estimated CO₂-saved figure — good talking points for the
  presentation

No backend, no signup. State is saved in the browser (`localStorage`), so it survives a
refresh but is local to your device — perfect for a live demo without a database.

> ⚠️ This is an academic demo. No real payment happens — the bKash/Rocket/Nagad/Upay
> screens simulate the flow only.

---

## Tech

Plain **HTML + CSS + JavaScript**, no build step, no dependencies. This is intentional:
it means the entire app is one file (`index.html`), it's trivial to explain in a viva,
and it deploys to Vercel with **zero configuration**.

---

## Run it locally

Just open `index.html` in a browser — or serve it so relative paths behave normally:

```bash
# Python
python3 -m http.server 5500
# then visit http://localhost:5500

# or, with Node
npx serve .
```

---

## Deploy: GitHub → Vercel

### 1. Push to GitHub

```bash
cd campus-cycle
git init
git add .
git commit -m "CampusCycle: campus bike-share demo for IDP-2"
git branch -M main
git remote add origin https://github.com/<your-username>/campus-cycle.git
git push -u origin main
```

(Create the empty `campus-cycle` repo on GitHub first via **New repository** — don't
initialize it with a README so the push above doesn't conflict.)

### 2. Deploy on Vercel

1. Go to [vercel.com](https://vercel.com) → **Add New… → Project**
2. Import the `campus-cycle` GitHub repo
3. Framework preset: **Other** (it's a static site — no build command needed)
4. Click **Deploy**

That's it — Vercel serves `index.html` directly. You'll get a live URL
(`campus-cycle-<hash>.vercel.app`) to put on your presentation slide and share with your
instructor.

---

## Presentation notes / talking points

- **Problem**: students walk long distances between campus buildings; cycles exist but
  there's no easy way to pay for casual, short-term use.
- **Solution**: dock-based cycle rental billed per minute, paid from a **prepaid wallet**
  topped up through the mobile wallets students already have — no cards, no cash, no app
  install (works in any browser).
- **Why a wallet, not pay-per-ride**: like a metro card — top up once, then every ride is
  a single tap with no repeat gateway login, no repeated transaction fees, and it works
  even for very short rides where a full gateway checkout would feel like overkill.
- **Why per-minute billing**: fair pricing for short hops (a 10-minute ride costs ~৳17,
  not a flat hourly rate).
- **Extendability** (mention as future work): real payment gateway integration (bKash
  Merchant API), GPS-based dock geofencing, QR-code unlock instead of a manual code,
  admin dashboard for facilities staff, and a login system tied to student ID.

## Project structure

```
campus-cycle/
├── index.html   # entire app: markup, styles, logic
└── README.md
```
