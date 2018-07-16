# GFF for data exchange

The Generic File Format for data exchange is, as the name itself describes,
a generic file format to pass data between two peers. Designed to be as small as
possible, includes a fast CRC32 calculation to check the data after the transfer.

## Format

It's a mix of fixed and variable length fields, as follows:

- UINT16 (2 bytes) Packet identifier (circular 0-255).
- UINT32 (4 bytes) Message type ID (unique per application) - [0x0000 - 0x0064] reserved.
- UINT32 (4 bytes) Number of fields.
- Field (repeated 0-n times)
  - String double-null-terminated (0x0000) - field name. Must not begin with 0x00.
  - Mixed double-null-terminated (0x0000) - field value.
    In case of number, the last two 0x00 values will be the terminating values.
    Must not begin with 0x00.
- CRC32 (4 bytes) of the entire message (but the last 4 CRC bytes)
