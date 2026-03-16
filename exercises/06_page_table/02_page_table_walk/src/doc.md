# Single‑Level Page Table Address Translation

This exercise simulates a simple single‑level page table to help you understand
the process of virtual‑to‑physical address translation.

## Concepts

- Virtual address = Virtual Page Number (VPN) + Page Offset (offset)
- Page table: VPN → PPN mapping table
- Address translation: Physical address = PPN × PAGE_SIZE + offset
- Page fault: accessing an unmapped virtual page

## Address Format (Simplified Model)

```text
Virtual address (32‑bit):
31          12 11          0
┌──────────────┬────────────┐
│   VPN (20 bits)  │ offset (12 bits) │
└──────────────┴────────────┘

Page size: 4KB (2^12 = 4096 bytes)
```
