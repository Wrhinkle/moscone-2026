# OpenClaw in Your Hand: Building a Physical AI Terminal
> A physicist at Callstack builds a battery-powered, dual-display hardware terminal for talking to OpenClaw and a local LLM on a DGX Spark, then discovers it makes a great text RPG console.

- **Speaker:** Lech Kalinowski, Callstack
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=akk6KRlcwW4) (AI Engineer channel; ~25m, released 2026-06-28)
- **Program:** Online Track 2026

## Summary
Kalinowski, who holds a PhD in physics and works in Callstack's technology incubator, opens with a staged story about finding an 80s-looking keyboard device in his basement that answers "who am I" in natural language. The real project: he wanted a remote controller for the OpenClaw instance running on his DGX Spark, and ended up building an AI-native physical terminal over about three months and 130 commits.

The core design decision is a dual-display approach. Electronic paper is ideal for reading but too slow for dynamically arriving text, so he pairs a small one-color OLED as the live surface for typing and streaming with an e-paper panel that renders the full page on enter. Rendering on a microcontroller forced constraints he walks through in detail: fixed static buffers, one-bit images in pre-allocated memory, no markdown engine, and no malloc on the MCU side. The hardware is an ESP32 dual-core microcontroller, OLED, keyboard, and rotary encoder, all powered by a single lithium polymer cell. He stresses the power management system because unstable current and voltage blew up two displays during prototyping. The firmware exposes four modes, including an internal shell for system settings and Wi-Fi, an assist mode for the LLM, and an RPG mode.

Because the device itself cannot run a model, a full backend handles the agentic work: firmware on the terminal talks to a backend that fronts OpenClaw and the LLM. For the demo he serves the open-source 120-billion-parameter GPT model on the DGX Spark with TensorRT and exposes it through an OpenAI-style proxy, after hitting walls with open models that do not match the OpenAI API shape. From the handheld he can issue commands like "write a Java example and store it on my local machine" and OpenClaw executes them.

His field notes are concrete hardware lessons: software I2C misbehaving without proper pull-ups, a silent failure on GPIO 13 that forced a port change, a regulator that killed the OLED and fragile display parts (replacement parts took weeks), and a cheap encoder whose rotational noise needed pull-ups and extra capacitors.

The part that surprised him is the RPG mode. He built a text-based role-playing experience with LLM-generated NPCs, memory, world mood, and four worlds (a cyberpunk one, a Witcher-style fantasy one, a deep-space void, and one more), with characters, maps, and skills generated and converted through the same one-bit rendering pipeline, 16 generatable classes in total. He argues there is a market niche for quiet, distraction-free AI hardware while everyone else builds around audio and video interfaces, and he has filed a provisional patent. The device is deliberately fault-tolerant: if the OLED fails the e-paper works, if the keyboard fails the encoder works, if Wi-Fi drops the local shell still runs. His closing joke lands on the irony that a text game with no 3D graphics is running on one of Nvidia's most advanced processors, and that the whole project is really a Game Boy for LLMs.

## Notable moments
- [0:03:06](https://www.youtube.com/watch?v=akk6KRlcwW4&t=186s) The dual-display idea: OLED as the fast live surface, e-paper as the bistable page render.
- [0:09:10](https://www.youtube.com/watch?v=akk6KRlcwW4&t=550s) Backend architecture: the 120B open model served with TensorRT behind an OpenAI-style proxy on the DGX Spark.
- [0:12:14](https://www.youtube.com/watch?v=akk6KRlcwW4&t=734s) RPG mode: four generated worlds and a pure text role-playing experience on e-paper.
- [0:18:41](https://www.youtube.com/watch?v=akk6KRlcwW4&t=1121s) Recorded demo: boot, Wi-Fi connect, checking disk space on the DGX Spark through OpenClaw, then gameplay.

## Connections
- [Nvidia](../../companies/models-inference/nvidia.md), whose DGX Spark and TensorRT serving stack host the model behind the terminal.
- [ClawLess paper](../../papers/tool-use-governance/clawless-a-security-model-of-ai-agents.md), a security model that names OpenClaw as a target system; relevant since this device gives OpenClaw shell-level reach over a home machine.
