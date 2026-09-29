# trustream

## What TRUSTREAM is

TRUSTREAM is compression for live data streams instead of files. Logs, traces, and telemetry flow through it in small 4 KB tiles as they arrive. Quiet stretches — the long runs of zeros and repetition that fill most logs — pack down small. Busy stretches pass through untouched, so the stream stays honest. Playback gives you the original bytes, in order.

Here is why that matters. Log volume grows faster than disk prices fall, and most teams pay three times over: to ingest it, to index it, and to keep it. A stream packer turns retention from a cost cliff into a feature — keep everything, pay for the packed size. The archive your auditors and your models both need gets dramatically cheaper to own.

Each tile goes through a short pipeline: the easy patterns first, then the math, then phrase matching, then storage. The cheap wins are tried before the expensive ones, so the stream keeps up in real time. And because it is lossless, a replayed event is the exact event — byte for byte.

It is aimed at agent fleets that log every tool call, observability stacks exporting packed telemetry, and on-device recorders — cars, drones, robots — that flush packed traces when they dock.

Reference implementation of the TRUSTREAM live tile pipe.

4 KiB tiles, frame = [tag:1][tile_len:u16 LE][payload].
ZERO (all-zero tiles), MATH (exact u8 ramps), PHRASE (reserved), STORE (raw).
Never expands: every tile's content encodes to <= its input size (3 B of framing per tile on top). Round-trip exact.
