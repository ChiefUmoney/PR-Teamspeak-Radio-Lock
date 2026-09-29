# Validation for 0.2.0

Passed with MSVC C++17, x64, static runtime, /W4 /WX, and assertions enabled:

1. Core regression tests: continuous one-hour grants for each of three simulated clients, including the coordinator; competing presses every 30 seconds; the holder never loses the grant from elapsed duration.
2. Busy indication: the contender is blocked and receives a busy flag, while the active speaker and other clients do not. A held denied key does not repeatedly alert or automatically transmit.
3. Release/rekey and existing parsing, authority, stale-grant, lease-expiry, and membership-change checks.
4. 100 randomized three-client network simulations with delayed, reordered, duplicated, and dropped control messages; at most one valid transmitter at every checked step.
5. Native DLL mock-host test: API 26 / version 0.2.0 exports, successful handshake, continuous 33-second transmission, busy.wav versus permit.wav selection through the local playback callback, gate closure on denial/controller loss, normal unmarked channels, channel transitions, and clean unload.
6. Package resource checks: custom busy.wav preserved, original permit.wav preserved, DLL and package version 0.2.0.

Live TeamSpeak voice and real network playback are not covered by these checks. The two-person procedure is in README.md.
