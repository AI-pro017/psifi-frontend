# PsiFi Frontend

The web app for PsiFi, a mobile style crypto wallet where you can send coins to other people by their username instead of a long wallet address.

It pairs with [psifi-backend](https://github.com/AI-pro017/psifi-backend), which handles accounts, creates the wallets and keeps each user's seed phrase encrypted.

## What you can do

- Sign up with a unique @username and a profile picture. The picture is uploaded to IPFS through Pinata.
- Get a wallet with addresses for Bitcoin, Ethereum, Solana, BNB Chain and Avalanche.
- See your total balance in USD, with live prices from CoinGecko and exchange rates for other fiat currencies.
- Open any coin to see its balance, a price chart and your recent transactions.
- Deposit by showing your address as a QR code.
- Send coins to a contact or any username, review the transaction before confirming and attach a short message.

Ethereum is the most complete flow right now. It runs on the Sepolia testnet, and the helpers for the other chains in `src/lib` point at their test networks too (Solana devnet, Avalanche Fuji and BNB testnet), so no real funds are involved.

## Tech stack

- Next.js 14 (App Router), React 18 and TypeScript
- Tailwind CSS with Radix UI components
- ethers, @solana/web3.js, bitcoinjs-lib and avalanche for the chain logic
- react-hook-form and zod for forms, ApexCharts for the price charts

## Running it locally

Start the backend first, then:

```bash
git clone https://github.com/AI-pro017/psifi-frontend.git
cd psifi-frontend
npm install
```

Create a `.env.local` file that points at the backend:

```env
NEXT_PUBLIC_BACKEND_API_URL=http://localhost:5000/api
NEXT_PUBLIC_PINATA_JWT=your-pinata-jwt
```

The Pinata JWT is used to upload profile pictures to IPFS during sign up. Use a scoped key that can only pin files.

Then run:

```bash
npm run dev
```

and open http://localhost:3000.

## Project structure

```
src/
  app/
    (auth)/       Login and register pages
    page.tsx      Home screen with total balance and coin list
    buy/          Coin detail page with chart, deposit and transactions
    send/         Send flow and success screen
  components/     UI pieces for each screen
  context/        Live coin prices
  lib/            Chain helpers for each network, IPFS upload and validators
  middleware.ts   Redirects to login when you're signed out
```
