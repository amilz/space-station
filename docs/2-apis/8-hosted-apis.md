---
sidebar_label: "Hosted APIs"
description: Run the swap API with one of Jupiter's Partner RPC nodes
title: "Hosted V6 Swap API"
---

High-volume, high-speed applications (e.g., liquidators, oracles, bots) can benefit from a hosted API with a private Solana RPC endpoint to entirely decouple their systems from Jupiter infrastructure.

Why consider a hosted API?

- **Reduced rate limits**: Integrators load is no longer restricted by the public API rate limits. Select a service that scales with your business needs.
- **Lower latency**: Get faster response times by running the API on a dedicated Solana RPC node.
- **Tailored Support**: Get support from the RPC provider to help you with your integration.

## Paid Hosted APIs

We are working with some Solana RPC partners who offer hosted APIs with the Jupiter Swap API:

- [QuickNode Metis - Jupiter V6 Swap API](https://marketplace.quicknode.com/add-on/metis-jupiter-v6-swap-api?utm_source=docs.jup.ag)

## Free Public Alternatives

If you prefer a free alternative to Jupiter's public API, you can try one of the following services (which may have different rate limits and performance characteristics):

- [JupiterAPI.com](https://www.jupiterapi.com/) by QuickNode

## Usage

To start using a hosted API, you will need to sign up for an account with the provider and follow their instructions to get started. Once you have an account, you will get a unique endpoint URL to use in your application, e.g., `https://example-jupiter-swap-api.quiknode.pro/123456`.


### Using HTTP Request

All you need to do to make HTTP requests to the hosted API is to replace the base URL in your requests with the endpoint URL provided by the provider. Here's an example of how to get a quote using the hosted API:

```ts
const jupiterEndpoint = `https://example-jupiter-swap-api.quiknode.pro/123456`;

async function getQuote() {
  const quoteResponse = await (
    await fetch(`${jupiterEndpoint}/quote?inputMint=So11111111111111111111111111111111111111112\
      &outputMint=EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v\
      &amount=100000000\
      &slippageBps=50`
    )
  ).json();
  // Handle quote response
}


```


### Using @jup-ag/api

Simpley pass your endpoint URL to the `createJupiterApiClient` function as a config object's `basePath` property. Here's an example of how to use the Jupiter API client with a hosted API endpoint:

```ts
import { QuoteGetRequest, QuoteResponse, createJupiterApiClient } from '@jup-ag/api';

const jupiterEndpoint = `https://example-jupiter-swap-api.quiknode.pro/123456`;
const config = {
    basePath: jupiterEndpoint
};
const jupiterApi = createJupiterApiClient(config);

// Example use
async function getQuote() {
  const quoteRequest: QuoteGetRequest = {
    inputMint: "EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v",
    outputMint: "So11111111111111111111111111111111111111112",
    amount: 10 * 1e6,
  }
     
  
  const quote: QuoteResponse | null = await jupiterApi.quoteGet(quoteRequest);
  // Handle quote response
}
```