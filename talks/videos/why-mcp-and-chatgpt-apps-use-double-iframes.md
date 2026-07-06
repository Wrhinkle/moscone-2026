# Why MCP and ChatGPT Apps Use Double Iframes

> A browser-security walkthrough of why third-party MCP app UI renders inside two nested iframes, and what app builders must do about CSP.

- **Speaker:** Frédéric Barthelet, Alpic
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=c-2eEv2ou7Y) (AI Engineer channel; ~20m, released 2026-06-15)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Barthelet, CTO and co-founder of MCP hosting company Alpic, opens with the puzzle that motivated the talk: inspecting ChatGPT's DOM, he found third-party app UI rendered inside an iframe nested in another iframe. The talk reconstructs why that design is the only workable one, by walking through each simpler option and showing how it fails.

Background first. MCP apps and ChatGPT apps add interactive views to conversational agents. A view is a plain HTML document with JS and CSS, advertised in tool metadata during the initial tools list call and rendered when the associated tool is called, with the tool result injected in. The mechanism was pioneered by MCP-UI, released by OpenAI as the Apps SDK in October, and standardized as the first official MCP extension. The same double-iframe structure appears on Claude.ai.

The elimination proceeds through content security policy. ChatGPT's CSP includes script-src, requiring every script to carry a per-request nonce, and frame-src, an allowlist of domains permitted to render in iframes. Option one, an iframe with the srcdoc attribute, inherits the parent's origin and CSP, so the app's scripts are blocked by the nonce rule. Relaxing the CSP would let the app run, but a same-origin iframe can then read ChatGPT's localStorage and cookies and ship them to the app developer's server. Adding the sandbox attribute gives the iframe a null origin, which stops the theft but also breaks localStorage, IndexedDB, and cookies for the app itself, and the only fix, allow-same-origin, reopens the sandbox escape. Option two, an iframe whose src points at each developer's own server, would force OpenAI to append every new app's domain to frame-src forever, which does not scale. Hosting all third-party UI on a single proxy domain works, and OpenAI does own openaiusercontent.com for this purpose, but serving arbitrary unreviewed third-party code from your own infrastructure is both a liability and an infrastructure burden most hosts cannot carry.

The double iframe threads the needle. The outer iframe loads one identical loader script for every app, served from a dedicated non-ChatGPT domain, so frame-src needs a single entry and the host serves only code it wrote. That loader spawns the inner iframe via srcdoc with the MCP resource content. Per-app subdomains on the loader domain keep origin-indexed storage from colliding between apps, so app ABC123 cannot read app ABC456's localStorage. A meta tag defined in the MCP app spec lets the view carry its own CSP. Barthelet notes the pattern is old: Facebook solved the same problem the same way for its app marketplace era.

The practical payload for builders: declare every domain your app depends on, connect-src for APIs you fetch, plus script, image, and frame sources, in the MCP app metadata, or your app breaks in production. OpenAI's developer mode used to strip all CSP, so builders discovered missing domains only after launch. Alpic's open source framework Skybridge adds end-to-end type safety between server and views, polyfills for host-specific APIs, and a CSP inspector that diffs the domains your view actually calls against the declared metadata live. He demos it with a magic eight ball app, adding an IP-lookup fetch and watching the inspector flag the missing domain instantly. He says CSP omissions are a common cause of ChatGPT app store rejections.

## Notable moments

- [0:03:09](https://www.youtube.com/watch?v=c-2eEv2ou7Y&t=189s) The surprise in ChatGPT's DOM: an iframe nested inside another iframe.
- [0:07:11](https://www.youtube.com/watch?v=c-2eEv2ou7Y&t=431s) Why srcdoc fails: shared origin means the nonce-based script-src blocks the app, and relaxing it exposes ChatGPT's localStorage.
- [0:11:14](https://www.youtube.com/watch?v=c-2eEv2ou7Y&t=674s) Why frame-src cannot allowlist infinite app domains, and the openaiusercontent.com proxy approach.
- [0:17:19](https://www.youtube.com/watch?v=c-2eEv2ou7Y&t=1039s) Skybridge demo, including the CSP inspector catching an undeclared API domain live.

## Connections

- [OpenAI](../../companies/models-inference/openai.md), whose ChatGPT app store, Apps SDK, and CSP architecture are the talk's main subject.
