Custom busy-sound edition of **Project Reality Radio Lock 0.1.0** for **TeamSpeak 3 on Windows 64-bit**.

When a user tries to transmit while the radio channel is occupied, the plugin's existing denial action now plays the supplied notification sound. Other existing busy/denial conditions use the same replacement sound.

### Download and install

Download **Project-Reality-Radio-Lock-0.1.0-custom-busy-win64.ts3_plugin** from the release assets. Close TeamSpeak, open the file to install or update, then restart TeamSpeak and enable the plugin under **Tools → Options → Addons → Plugins**.

Keep `[PR-RADIO]` in protected channel topics. Every participating user must have the radio-lock plugin enabled. Keep your normal push-to-talk binding.

### Changed

- Custom busy sound, converted to 16-bit mono 48 kHz PCM.
- No changes to the locking logic or permit beep.

### Validation

Verified the package contents, unchanged DLL and other resources, and valid non-silent WAV output. Live two-user playback remains untested; use this as a **pre-release** and test before a patrol.

The plugin itself continues to report version **0.1.0**. This tag identifies the sound-only edition. Original plugin source code is not included.
