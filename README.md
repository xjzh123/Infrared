# ⛅️ Infrared

> Why bring the user to the proxy, when you can bring the proxy to the user?
>
> - bomberfish, 2023 (colourized)

Advanced web proxy based on [TompHTTP Bare Server](https://github.com/tomphttp/bare-server-worker), hosted on Cloudflare Workers.

This version serves the frontend in the worker too, so that you don't need to host the frontend and the backend separately. Just deploy it to one worker, and you can enjoy your proxy.

(CF Workers can serve static files [with hono](https://hono.dev/docs/getting-started/cloudflare-workers#serve-static-files). However, it is deprecated in favor of CF Pages. But now that Infrared is a proxy for CF Workers, it is better and easier to migrate the frontend assets to the worker, instead of migrating the backend to Pages.)

Also, the original frontend has its backend URL hard coded, but with this version, the frontend uses your own backend run in your own worker.

## Deploy

First, clone this repo. Then clone the frontend submodule:


```sh
git clone
git submodule init
git submodule update
```

Then install dependencies:

```sh
npm install
```

After this, you may need to login at `wrangler` with `npx wrangler login`.

Then create a KV database namespace named `BARE`:

```sh
npx wrangler kv namespace create BARE
```

After this, edit `wrangler.toml` to use your own KV namespace.

Finally, you can deploy to cloudflare.

```sh
npx wrangler deploy
```

Note that although these commands use `npm` and `npx`, if you have `pnpm`, it is better to use `pnpm` instead of `npm` and `npx` for this repo.
