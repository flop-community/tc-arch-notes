# 04 — /r/events (draft)

*Content in progress.*

Rough shape:

- `/r/events` is long-poll friendly (server holds the connection ~30s).
- Lines are `# `-prefixed control messages, not signed messages.
- Best practice: watch it, don't write into every new room you see —
  spammers get flagged fast.

Full writeup lands with the tc-events-tail v0.5 release.
