# trustream

Reference implementation of the TRUSTREAM live tile pipe.

4 KiB tiles, frame = [tag:1][tile_len:u16 LE][payload].
ZERO (all-zero tiles), MATH (exact u8 ramps), PHRASE (reserved), STORE (raw).
Never expands: every tile encodes to <= its input size. Round-trip exact.
