# Project Reality Radio Lock

**TeamSpeak 3 · Windows 64-bit · Custom busy sound · Pilot release**

One-at-a-time radio transmission for cooperating TeamSpeak users. This edition replaces the original busy tone with a custom notification sound: when a user tries to key up while the channel is occupied, the existing radio-lock logic denies the transmission and plays the sound locally.

This is a sound-only update to plugin version **0.1.0**. The compiled plugin and permit beep are unchanged.

## Download

Open this repository's **Releases**, select **v0.1.0-custom-busy**, and download this file under **Assets**:

`Project-Reality-Radio-Lock-0.1.0-custom-busy-win64.ts3_plugin`

GitHub's automatic **Source code (zip)** download is not the plugin installer. Download the `.ts3_plugin` attachment instead.

## Install or update

1. Close TeamSpeak 3.
2. Open the downloaded `.ts3_plugin` file and install it. When updating, allow the existing plugin files to be replaced.
3. Reopen TeamSpeak 3.
4. Enable **Project Reality Radio Lock** under **Tools → Options → Addons → Plugins**.
5. Keep your normal **Push-To-Talk** binding. Disable **Add Voice Activity Detection** if selected.

Requires Windows 64-bit and a TeamSpeak 3 client supporting plugin API 26, such as TeamSpeak 3.6.2. This is not a TeamSpeak 6 plugin.

## Enable a channel

A server administrator should add this marker to the channel's **Topic**:

```text
[PR-RADIO]
```

For example: `[PR-RADIO] County Dispatch`.

Every participating user must have the radio-lock plugin enabled. Each user who wants the replacement sound should install this edition. Mark each protected channel separately; protection does not inherit into subchannels.

## Use the radio

- After joining a protected channel, release PTT and wait about three seconds.
- Hold PTT and wait for the permit beep before speaking.
- If you hear the busy sound, release PTT. Press again after the other user finishes. Holding a denied key does not automatically begin transmission later.
- Release PTT to free the channel. The existing plugin limits each transmission to 30 seconds.
- Use normal same-channel PTT. Whisper lists and cross-channel transmissions are not covered.

The plugin also uses the busy sound when the coordinator is unavailable or another existing denial condition occurs. This edition preserves those triggers.

## Test before using it for a patrol

1. Two users install and enable the plugin, then join a marked test channel.
2. Both release PTT and wait three seconds.
3. User A holds PTT, waits for permission, and speaks.
4. While A talks, user B presses PTT. B should hear the replacement sound; A should not hear B transmitting.
5. After A releases PTT, B releases and presses again. B should receive permission.

This is cooperative client protection. A user without the plugin can still transmit. The original plugin elects the human client with the lowest TeamSpeak client ID as coordinator, so all channel members need the plugin enabled.

## What changed

Only `plugins/pr_radio_lock/busy.wav` inside the installer was replaced. The supplied notification was converted to **16-bit mono PCM, 48 kHz**, matching the original resource format. Its duration is approximately **0.109 seconds**.

The DLL, permit sound, package metadata, and original bundled README were verified unchanged by SHA-256 comparison. WAV structure and non-silent output were checked. **Live two-user TeamSpeak playback has not been tested for this edition.**

The original bundled README describes the pilot plugin's original tests. Those historical claims are distinct from the checks performed for this sound update.

## Troubleshooting

- **No sound:** confirm the plugin is enabled, check TeamSpeak playback volume, and reinstall this edition to replace the old `busy.wav`.
- **Repeated busy sound:** release PTT, wait three seconds, and check that all channel members have the plugin enabled.
- **No locking:** confirm `[PR-RADIO]` is in the channel topic, not its description or name.
- **Diagnostics:** enter `/prradio status` in TeamSpeak's chat input. This is a local plugin command.

## Repository contents

- `assets/busy.wav`: the converted replacement sound.
- `CHANGELOG.md`: changes in this edition.

https://github.com/ChiefUmoney/PR-Teamspeak-Radio-Lock/releases/tag/radio-lock
- `RELEASE-NOTES.md`: release description.

This repository distributes a compiled plugin with a replacement audio resource. **The original plugin source code was not supplied and is not included.** The plugin still reports version 0.1.0; the GitHub tag identifies the custom sound edition.
