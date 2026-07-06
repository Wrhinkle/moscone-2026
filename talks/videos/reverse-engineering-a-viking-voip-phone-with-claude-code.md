# Reverse engineering a Viking VOIP phone protocol with Claude Code
> How Boris Starkov used Claude Code to reverse engineer an undocumented VOIP phone so it could talk to an ElevenLabs voice agent.

- **Speaker:** Boris Starkov, ElevenLabs
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=V-L0INGTEOg) (AI Engineer channel; ~20m, released 2026-05-29)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary
Boris Starkov walks through a hardware reverse engineering project he ran mostly by giving Claude Code the keyboard. ElevenLabs built a red phone booth demo for the summit, on the third floor of the venue, where a visitor picks up a retro Viking VOIP phone and talks to an AI agent using an approved Michael Caine voice that quizzes them on British AI history. The hard part was the phone. The unit only shipped with Windows XP era software, and nobody at ElevenLabs runs Windows. A year earlier, three senior engineers plus ChatGPT had failed to make the same phone work, so it sat unused until this project.

The target architecture is simple to state. The Viking phone can only dial a phone number, so Twilio sits in the middle to handle SIP trunk complexity, then routes to the ElevenLabs conversational agent. Getting the phone to dial out was the blocker. Starkov connected the phone over Power over Ethernet through a router, put his Mac on the same network, and let Claude Code explore. Claude ran nmap, found the wrong port first (an "electronics tunnel" on 1001), then the real control port. It sent test strings and noticed the phone replied with "ER" plus the echoed string, an error response, which told Claude this was a real command interface with no public documentation.

Claude then brute forced the protocol. It learned commands were two letters, iterated every two-letter combination, and found roughly 80 valid commands out of the full space, some legible like SA for status. It could write credentials into the phone's memory so the phone knew to call the Twilio SIP trunk, but every setting vanished on reboot because it was writing to temporary memory. This persistence problem was exactly where the earlier team had given up a year before. Claude did not stop. It set up a Windows virtual machine to run the vendor software, worked around the fact that macOS cannot bridge Wi-Fi into the VM by running a TCP proxy on the Mac that relayed and logged all traffic between the vendor software and the phone. That man-in-the-middle capture revealed a TS command carrying a binary payload whose fields were readable except for a one-byte checksum. Because Claude knew the input data and the result, it reverse engineered the checksum as a simple one-byte addition and confirmed it by running more values through the loop.

With the protocol cracked, Starkov factory reset the phone and programmed it directly, no VM required, then packaged the whole method as an open-sourced Claude skill so anyone with the same phone can skip the Windows setup. He estimates the effort cost between 10 and 100 dollars in ElevenLabs tokens and took a couple of days. His framing is that a year ago you needed the vendor's proprietary interface, and now you can connect to arbitrary hardware the same way. In the Q&A he says his own role was to be Claude's hands, physically rebooting the phone and counting beeps, while Claude did the intellectual work he could not have done himself as a non-security engineer.

## Notable moments
- [0:04:10](https://www.youtube.com/watch?v=V-L0INGTEOg&t=250s) Claude nmaps the ports and identifies the real control interface by the "ER" error echo.
- [0:06:10](https://www.youtube.com/watch?v=V-L0INGTEOg&t=370s) Brute forcing all two-letter commands surfaces about 80 valid ones.
- [0:09:12](https://www.youtube.com/watch?v=V-L0INGTEOg&t=552s) The TCP proxy man-in-the-middle trick captures the vendor software's traffic to break persistence.
- [0:17:13](https://www.youtube.com/watch?v=V-L0INGTEOg&t=1033s) Starkov describes himself as the hands for Claude, following its instructions to reboot and listen for beeps.

## Connections
- [Twilio](../../companies/voice-realtime/twilio.md) provides the SIP trunk that bridges the Viking phone to the ElevenLabs agent, and built the phone booth demo.
