# PartyKit on Cloudflare for a Personal Website

**Date:** 2026-04-14  
**Category:** engineering  
**Tags:** `cloudflare`, `partykit`, `realtime`, `websockets`, `durable-objects`  
**Related:** *(none yet)*

---

## TL;DR

- PartyKit is a real-time app platform built on Cloudflare's `workerd` runtime and backed by Durable Objects, so it is a strong fit for stateful WebSocket features on a personal site
- The core model is simple: each room or feature instance gets an `id`, and PartyKit routes every connection for that `id` to the same stateful server instance
- For a personal website, PartyKit is a good match for live presence, reactions, shared cursors, lightweight chat, collaborative widgets, and other low-latency features
- Start with `npm create partykit@latest`, run locally with `npx partykit dev`, and deploy with `npx partykit deploy`
- Do not commit secrets, tokens, or account-specific values into this repo; use placeholders in code samples and keep real credentials in your deployment platform

---

## Understand what PartyKit is

PartyKit is a platform for building **real-time**, **multiplayer**, and **stateful** applications using standard web primitives like HTTP and WebSockets. Under the hood, each PartyKit room is backed by a **Cloudflare Durable Object**, which means the platform can keep room-specific state together with the code handling that room.

That matters because it removes a lot of the plumbing you would otherwise need for:

- coordinating multiple WebSocket clients
- deciding where state lives
- routing messages to the correct room
- scaling room instances without manually managing servers

Instead of building a generic WebSocket server and inventing your own routing model, you usually think in terms of:

- **one PartyKit server class**
- **one room type**
- **one room id per document, page, post, feature, or session**

---

## Map the PartyKit model to a personal website

For a personal site, PartyKit is most useful when a page needs shared state or low-latency communication between visitors.

Good fits:

- live visitor presence on a page
- synchronized reactions during a livestream or launch post
- a lightweight chat room for a page or event
- collaborative notes, whiteboards, or text editing
- live status widgets for AI agents or background jobs

A useful mental model is:

| Website concept | PartyKit concept |
|---|---|
| Blog post, page, event, or shared widget | Room id |
| Realtime backend for that page | Party |
| Browser tab connected to the feature | WebSocket connection |
| Shared mutable state | Durable Object-backed room state |

If a feature does not need shared state or push updates, PartyKit is probably unnecessary. If it does, PartyKit is often simpler than wiring raw Workers, a hosted pub/sub system, and a separate state store yourself.

---

## Understand the request and room model

PartyKit gives you both HTTP and WebSocket entry points.

- Use **`onRequest`** when you want an HTTP response for a room
- Use **`onConnect`** and **`onMessage`** for live bidirectional behavior
- Use the room `id` to scope state to a page, document, or feature instance

Because PartyKit routes all connections for the same `id` to the same room instance, you can write logic as if that room owns its own isolated state.

That is the key simplification.

---

## Start with the standard PartyKit workflow

Create a new project:

```powershell
npm create partykit@latest
```

Run it locally:

```powershell
npx partykit dev
```

Deploy it:

```powershell
npx partykit deploy
```

PartyKit provisions a hosted endpoint for the project, and the same room model works locally and after deployment.

---

## Use a minimal starter pattern for a personal site

For a personal website, a small presence or reactions feature is a good first implementation because it exercises the important parts of the platform without forcing you to solve auth, storage, moderation, and replay history on day one.

Example server:

```ts
import type * as Party from "partykit/server";

export default class Server implements Party.Server {
  constructor(readonly room: Party.Room) {}

  countConnections() {
    return [...this.room.getConnections()].length;
  }

  announcePresence() {
    this.room.broadcast(
      JSON.stringify({
        type: "presence",
        online: this.countConnections()
      })
    );
  }

  onConnect() {
    this.announcePresence();
  }

  onClose() {
    this.announcePresence();
  }

  onMessage(message: string, sender: Party.Connection) {
    this.room.broadcast(
      JSON.stringify({
        type: "message",
        value: message
      }),
      [sender.id]
    );
  }

  onRequest() {
    return Response.json({
      roomId: this.room.id,
      online: this.countConnections()
    });
  }
}
```

Example client connection:

```ts
const ws = new WebSocket(
  "wss://<your-project>.<your-username>.partykit.dev/parties/main/homepage"
);

ws.addEventListener("message", (event) => {
  const data = JSON.parse(event.data);
  console.log(data);
});

ws.send("hello from the site");
```

Notes:

- `homepage` is the room id in this example
- replace placeholders like `<your-project>` and `<your-username>` with your real deployment values outside this public KB
- if you want one room per blog post, use a stable room id such as the post slug

---

## Keep public-repo boundaries clear

Because this knowledge base is public, keep the article and future implementation notes safe to publish:

1. Never commit API keys, tokens, cookies, or account identifiers that should remain private.
2. Keep code samples generic and use placeholders such as `<your-project>` instead of real values.
3. Treat room ids as public identifiers unless you add your own authorization checks.
4. If a feature should be private or member-only, gate it in `onBeforeConnect` or `onBeforeRequest` rather than relying on an unguessable room id.

PartyKit supports secret management in its workflow, but those secret values belong in the deployment environment, not in this repository.

---

## Practical starting point for your website

If the goal is to add PartyKit to a personal site without overbuilding, the safest progression is:

1. Add a **page presence** feature first
2. Add **reactions or lightweight messages** second
3. Add **persistence, auth, or moderation** only after the realtime path works well

That sequence keeps the first implementation small while still teaching the important PartyKit concepts: room ids, connection lifecycle, broadcasts, and room-scoped state.

---

## Sources

[1] [PartyKit Docs](https://docs.partykit.io/)  
[2] [PartyKit Quickstart](https://docs.partykit.io/quickstart/)  
[3] [How PartyKit works](https://docs.partykit.io/how-partykit-works/)  
[4] [Party.Server API](https://docs.partykit.io/reference/partyserver-api/)  
[5] [Cloudflare Durable Objects](https://developers.cloudflare.com/durable-objects/)  
[6] [PartyKit Homepage](https://www.partykit.io/)
