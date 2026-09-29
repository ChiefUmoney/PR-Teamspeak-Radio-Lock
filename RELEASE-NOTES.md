# Project Reality Radio Lock 0.2.0 — No Transmission Cutoff

- Removed the 30-second transmission limit. A healthy radio grant now renews for as long as PTT is held.
- Kept one-user-at-a-time locking. Simultaneous requests result in one grant; other users are blocked.
- Preserved the supplied custom busy sound, played locally to the user whose request is denied. It does not interrupt the current speaker.
- A denied key must be released and pressed again. No automatic transmission or repeated sound while it remains held.
- Preserved the permit beep, connection recovery, and stale-lock protection.

Close TeamSpeak, install **Project-Reality-Radio-Lock-0.2.0-win64.ts3_plugin**, reopen it, and confirm version **0.2.0** in Addons. Upgrade every participant. Keep `[PR-RADIO]` in protected channel topics and use normal same-channel push-to-talk.

This release includes source and tests recovered from the matching original build. Automated simulations and a DLL mock-host test are included; live two-user playback still needs verification. Publish as a pre-release until that check is complete.
