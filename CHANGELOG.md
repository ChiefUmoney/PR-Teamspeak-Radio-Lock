# Changelog

## 0.2.0 — No transmission cutoff

- Removed the hard-coded 30-second transmission cap. Grants continue renewing while the speaker holds PTT and the connection is healthy.
- Kept exclusive radio ownership, denied-key latching, and the custom local busy sound.
- Added long-transmission and contention regression checks: three one-hour simulations, plus a real compiled DLL held for 33 seconds against a mocked TeamSpeak host.
- Verified that healthy renewals do not play repeated sounds and that only the contender receives the busy alert.
- Preserved connection-loss recovery and stale-grant protections.
- Recovered matching original source and included buildable source and tests.

## 0.1.0 custom busy sound

- Replaced busy.wav with the supplied notification sound, converted to 16-bit mono 48 kHz PCM.
- Kept the original DLL and its 30-second cap. That cap is removed in 0.2.0.
