# BuyerBench registrations

Pre-registration records for BuyerBench studies. BuyerBench is a working name.

Each study is frozen before any study run. Its protocol, code, question set, product data and run settings
are hashed into one manifest, and the manifest's fingerprint is published here with an OpenTimestamps proof
anchored in Bitcoin, which does not depend on this repository or on GitHub. The manifest and the questions
stay private until the study's results are published, so the questions cannot leak into model training
data; from then on, anyone can check them against the fingerprint.

| Study | Frozen | Fingerprint (sha256) | Timestamp proof |
|---|---|---|---|
| S01 | 2026-09-22 | `4b69409d955bc95a149d7677b850029934ef5b1bf865a4ee302500b903638c19` | [`s01/PREREGISTRATION.txt.ots`](s01/PREREGISTRATION.txt.ots) |
| S01, addendum 1 | 2026-10-11 | `aaf9bedb71a5c82b39735685a5d76451817b79e34fbb1d593604297ea26fb7eb` | [`s01-addendum-01/PREREGISTRATION.txt.ots`](s01-addendum-01/PREREGISTRATION.txt.ots) |

## Verifying

- **When it was registered:** `ots verify <study>/PREREGISTRATION.txt.ots` with the OpenTimestamps client, or
  drop the `PREREGISTRATION.txt` file and its `.ots` file on opentimestamps.org.
- **Study 01's timing, stated plainly:** its proof is anchored in Bitcoin block 968220 (03:35 UTC on 2026-09-23),
  about an hour after the main run began (02:23 UTC). What shows the fingerprint came first is this repository's
  push at 02:23:45 UTC. Later studies start their main run only after the Bitcoin confirmation.
- **What was registered,** once results are out: the manifest `FREEZE.json` is published with the results.
  Remove its `fingerprint_sha256` field and take the sha256 of the rest serialised as
  `json.dumps(manifest, sort_keys=True, separators=(",", ":"))` (Python). It must equal the fingerprint above,
  and every file the manifest lists must match its own sha256.
- No study run may precede the timestamp.
