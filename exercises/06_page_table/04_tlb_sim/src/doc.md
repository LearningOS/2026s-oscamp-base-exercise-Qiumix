# TLB 模拟与刷新

本练习模拟 TLB（Translation Lookaside Buffer，地址翻译后备缓冲区），
帮助你理解 TLB 的查找、插入、替换和刷新机制。

## 知识点

- TLB 是页表的硬件缓存，加速虚拟地址翻译
- TLB 命中/未命中（hit/miss）
- TLB 替换策略（本练习使用 FIFO）
- TLB 刷新：全部刷新、按虚拟页刷新、按 ASID 刷新
- ASID（Address Space Identifier）区分不同进程的地址空间
- MMU 工作流程：先查 TLB，miss 则走页表，再回填 TLB

## TLB 条目结构

```text
┌───────┬──────┬──────┬───────┬───────┐
│ valid │ asid │ vpn  │  ppn  │ flags │
└───────┴──────┴──────┴───────┴───────┘
```
