# ShengUfs

> ## ⚠️ 本 fork 已停更（2026-11-16 更新）
>
> **这是 `UniXNU/ShengUfs` 的 fork，冻结在 2026-10-24，仅为向上游提 PR 保留。**
>
> **nabu 的现行 UFS 实现在 [`unixnu-nabu`](https://github.com/Lux12138/unixnu-nabu)
> 的 `drivers/NativeUfs/`，不要用本仓库做集成。**
>
> | 版本 | `NativeUfs.cpp` | 时间 | 说明 |
> |---|---:|---|---|
> | 本 fork | 85 KB | 2026-10-24 | 上游 SM8550 版，未含任何 nabu 改动 |
> | 板侧现行 | 250 KB | 2026-11-05 | 实际在跑的版本，见下 |
>
> 板侧在 fork 之后新增的能力（本仓库都没有）：
>
> - `NABUDIAG` 双槽诊断导出（220 s / 300 s，含 tracev3 + uuidtext + `screen.bgrx`）
> - `NABULOG1` 每 2 秒尾部写窗口（`autolog` v38 的落盘侧）
> - `nabu-dpu=1/2` MDP/VIG 只读探针
> - WDT pet 路径（`pet=600` + `nabu-wdt-arm-delay=0` 的自动回 TWRP）
> - `writable[]` 属主表：`/private/var/installd` 33:33、`/Library/Keychains` uid 64
> - 导出区几何（`kExportBlocks = 65536`，位于日志窗口下方 256 MiB）
> - 诊断导出区与启动参数面（`nabu-log` / `nabu-diag-at0/1` / `nabu-ufs-*` 等）
>
> ### 保留这个 fork 的唯一目的
>
> 其中一部分改动是**通用**的，与 nabu 无关，值得回流上游
> `UniXNU/ShengUfs`：诊断导出区的目录遍历与预算分配逻辑、
> `NABULOG1` 的尾部块写形式、以及 `IONewData` 失败时的两遍扫描模式。
> fork 保留就是为了将来能从板侧实现里挑出这些，向上游提 PR。
>
> 注意上游本身已大幅前进（2026-11-15 仍有
> `fix(storage): restore ShengUfs root window layouts`、
> `feat(storage): support APFS container store layouts`、
> `perf(ufs): cache verified-root table pages`），
> 提 PR 前必须先 rebase 到当前 upstream。

---

SM8550 UFS transport and sheng persistent storage.

the native UFS root works on sheng.

Build and interface details: [documentation](https://unixnu.com/drivers/sheng-ufs). Component sources and dependencies: [catalog](https://unixnu.com/reference/components).
