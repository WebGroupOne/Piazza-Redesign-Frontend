# Piazza Redesign

Codebase for Piazza Redesign.

## Setup

1. Build the packages

```sh
yarn build
```

2. Run locally and view in your browser

```sh
yarn dev
```

### Minor Note

To speed up build/runtimes, you'll want to link it to a turbo cache via:

```sh
npx turbo login
```

And then after you authenticate with Vercel:

```sh
npx turbo link
```
