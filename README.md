# Project Reality Radio Lock 0.2.0

**TeamSpeak 3 · Windows 64-bit · No transmission duration cutoff**

Hold push-to-talk for as long as you need. The first granted user keeps the radio until they release PTT. If another user tries to key up while it is occupied, that user's transmission is blocked and **only that user hears the supplied busy sound**.

If users press at the same time, the coordinator grants one request and denies the others. A denied user must release PTT and press again after the current speaker finishes. Continuing to hold a denied key does not start transmitting automatically and does not repeatedly play the sound.

## Install or update

[Download the 0.2.0 installer](https://github.com/ChiefUmoney/PR-Teamspeak-Radio-Lock/raw/refs/heads/main/Project-Reality-Radio-Lock-0.2.0-win64.ts3_plugin).

The earlier [radio-lock release](https://github.com/ChiefUmoney/PR-Teamspeak-Radio-Lock/releases/tag/radio-lock) contains the old 0.1.0 build. Use the 0.2.0 download above for unlimited transmission duration.

1. Close TeamSpeak 3.
2. Open **Project-Reality-Radio-Lock-0.2.0-win64.ts3_plugin** and install/update it, allowing the old plugin files to be replaced.
3. Reopen TeamSpeak. Enable **Project Reality Radio Lock** under **Tools → Options → Addons → Plugins**. Its version should be **0.2.0**.
4. Keep **Push-To-Talk** selected with your usual key or mouse button. Disable **Add Voice Activity Detection** if selected.
5. Have every channel member upgrade to this version.

Requires a 64-bit TeamSpeak 3 client supporting plugin API 26, such as TS3 3.6.2. This is separate from the PR Radios overlay and its bridge.

## Protect a channel

Add **`[PR-RADIO]`** to the channel's **Topic**, for example `[PR-RADIO] County Dispatch`. Each protected channel needs its own marker. Ordinary unmarked channels retain normal TeamSpeak behavior.

The human client with the lowest TeamSpeak client ID coordinates permission requests. Every person in a protected channel must have the plugin enabled. This is cooperative client protection; it cannot prevent someone using an unmodified or disabled client from transmitting.

## Use

- On joining a protected channel, release PTT and allow about three seconds for the group to settle.
- Hold PTT, wait for the permit beep, then speak. There is **no 30-second limit or other maximum transmission duration**.
- Release PTT to free the radio. There is a short turnaround gap between speakers.
- A busy sound means release PTT and try again once the radio is clear.
- Holding PTT keeps the radio reserved even during a pause in speech.

Normal same-channel PTT is supported. Whisper lists and cross-channel transmissions are not arbitrated. Native hotkeys and stored mute settings are not changed.

## Connection recovery

Connection-health checks remain. A lost coordinator, expired grant, channel change, membership change, or capture failure can close the microphone gate and require a new key press. These checks prevent simultaneous grants or a stale radio lock after a disconnect; they do not impose a length limit on a healthy transmission.

The supplied busy sound is also used for existing unavailable-controller and denied-request conditions. It plays locally through TeamSpeak's playback device, not into the voice channel. The permit beep is unchanged.

## Verify with two people

1. Both users install 0.2.0, enter a marked test channel, release PTT, and wait three seconds.
2. A presses PTT, waits for the permit beep, and holds it for over one minute while speaking periodically. There should be no duration cutoff.
3. While A is holding PTT, B presses PTT. B should hear the custom sound; A should not hear B transmitting or B's notification.
4. A releases PTT. B must release and press again to obtain the radio.
5. Try simultaneous presses several times: only one user should get permission.
6. Check that a disconnected coordinator closes the gate and that the remaining users can rekey after the group settles.

## Troubleshooting

- Enter `/prradio status` in TeamSpeak's chat input for local status.
- If an old 30-second cutoff remains, confirm the transmitting user's installed plugin version is 0.2.0 and restart TeamSpeak after updating.
- Repeated denials: release PTT, wait for the channel to clear, and confirm every participant is running this plugin in native PTT mode.
- Missing notification: check TeamSpeak's playback device and volume and reinstall the package so both WAV files are present.

## Build and tests

[Download the matching source and tests](https://github.com/ChiefUmoney/PR-Teamspeak-Radio-Lock/raw/refs/heads/main/Project-Reality-Radio-Lock-0.2.0-source.zip), extract the ZIP, then run **Build.ps1** in Windows PowerShell with Visual Studio C++ Build Tools and a Windows SDK installed. It compiles with warnings treated as errors, runs the core simulation and DLL smoke tests, and packages the installer. The DLL test intentionally holds a simulated PTT press for over 30 seconds, so the full build takes around a minute.

Tests cover three simulated one-hour transmissions, contention during long transmissions, sound only on the denied node, one alert per denied press, release/rekey, lease recovery, stale grants, membership changes, and 100 randomized network simulations. The compiled DLL is checked for a continuous 33-second grant, local sound selection, microphone gating, denied-key latching, controller loss, normal channels, and shutdown.

These are automated and mocked-host checks. **A real two-user TeamSpeak voice session has not been tested here.**

The original source was recovered from an earlier local project whose DLL SHA-256 exactly matched the supplied 0.1.0 plugin. API headers come from the [official TeamSpeak plugin SDK](https://github.com/teamspeak/ts3client-pluginsdk), with original header notices retained.
