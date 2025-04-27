# CorePerf
# CorePerf

**Table 1: Application Processor (AP) Core Comparison**

| Vendor   | Product Model               | Architecture                                  | Category                 | Key Configuration                                                                                                                                                                        | Performance Metrics                                                                                                                                                                                                                                          | Remarks                                                                                                                                                                                                                                                                                                                                        |
| -------- | --------------------------- | --------------------------------------------- | ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ARM      | Cortex-A720                 | Armv9.2-A (AArch64 only)                      | AP Core                  | OoO, Superscalar, 64KB L1 I/D Cache, 256KB-512KB Private L2 (typ), Opt. L3 (DSU-120), SVE2, PAC (QARMA3), MTE                                                                            | 20% efficiency gain vs A715.[^1] SPECint2k6/GHz: \~5.7 (Est. based on [^2]). CoreMark/DMIPS: N/A in sources.                                                                                                                                                 | Premium efficiency core. Target: Mobile (Premium AAA Gaming), Laptops, 5G. Pairs with A520/X4 in DSU-120. Area \~0.8mm² (core).[^2] Product Page: [https://www.arm.com/products/silicon-ip-cpu/cortex-a/cortex-a720][^1]                                                                                                                       |
| ARM      | Cortex-A520                 | Armv9.2-A (AArch64 only, Harvard)             | AP Core                  | In-Order, Superscalar (Merged-core complex up to 2 cores/complex), 32/64KB L1 I/D Cache, Opt. 128KB-512KB L2, Opt. L3 (DSU-120, 256KB-32MB), SVE2, PAC (QARMA3), MTE, ECC                | 8% perf uplift, 22% efficiency gain vs A510.[^3] SPECint/CoreMark/DMIPS: N/A in sources. Geekbench 6 (Exynos 2400): SC: 352, MC: 1048 (4 cores).[^4]                                                                                                         | High-efficiency core. Target: Mobile background tasks, Consumer devices. Pairs with A720/X4 in DSU-120. Product Page: [https://developer.arm.com/Processors/Cortex-A520][^3]                                                                                                                                                                   |
| ARM      | Cortex-A78                  | Armv8.2-A (AArch32 at EL0 only)               | AP Core                  | OoO, Superscalar, 64KB L1 I/D Cache, 256KB-512KB Private L2, Opt. L3 (512KB-4MB), ACE/CHI bus                                                                                            | DMIPS/MHz: \~7.3 (Est. based on [^5]). SPECint/CoreMark: N/A in sources. PassMark (4 Core @ \~2GHz): CPU Mark \~3000-3500, Single Thread \~1100-1470.[^6] [^7] +7% IPC vs A77.[^8] +8-13% SPECint/fp vs SD865 A77.[^9]                                       | High performance core for mobile/infrastructure. Predecessor to A710/A715/A720. Product Page: [https://developer.arm.com/Processors/Cortex-A78][^10]                                                                                                                                                                                           |
| ARM      | Cortex-A55                  | Armv8.2-A                                     | AP Core                  | In-Order, Superscalar, 8-64KB L1 I/D Cache, 64KB-256KB Private L2, Opt. L3 (256KB-4MB), ACE/CHI bus                                                                                      | DMIPS/MHz: \~2.3-3.0.[^5] CoreMark/SPECint: N/A in sources. PassMark (8 Core @ 1.8GHz): CPU Mark \~3013, Single Thread \~959.[^11] PassMark (4 Core @ 2.1GHz): CPU Mark \~676, Single Thread \~311.[^12]                                                     | High-efficiency core, often paired with A7x series. Product Page: [https://developer.arm.com/Processors/Cortex-A55][^13]                                                                                                                                                                                                                       |
| ARM      | Neoverse V3 (Poseidon)      | Armv9.2-A (AArch64 only)                      | AP Core (Infrastructure) | OoO, Superscalar, 64KB L1 I/D Cache (coherent), Private L2 (2MB 8-way or 3MB 12-way), 48-bit PA, SVE2, RME, MTE, RAS, CHI.E bus                                                          | Double-digit perf uplift vs V2.[^14] Benchmarks N/A in sources.                                                                                                                                                                                              | Highest performance Neoverse core. Target: Cloud, HPC, AI/ML, Confidential Computing. Product Page: [https://www.arm.com/products/silicon-ip-cpu/neoverse/neoverse-v3][^14], [https://developer.arm.com/Processors/Neoverse%20V3][^15]                                                                                                         |
| ARM      | Neoverse N2 (Perseus)       | Armv9.0-A (AArch64 only, Cortex-A710 derived) | AP Core (Infrastructure) | 10-stage pipeline, 5-wide Rename/Dispatch, 160+ ROB, 64KB L1 I/D Cache, up to 1MB Private L2 (ECC), up to 64MB Shared L3 (SLC), SVE2, CMN-700 mesh                                       | SPECrate®2017_int_base: \~250 (64T@3.0GHz, 5nm).[^16] Matrix Ops/cycle/core: 128 INT8, 64 BF16.[^17] 40% scalar perf uplift vs N1.[^18] PassMark (8 Core @ 2.5GHz): CPU Mark 5544, Single Thread 1361.[^19] CoreMark/DMIPS: N/A in sources.                  | High efficiency infrastructure core. Target: Datacenter, 5G, Networking, Scale-out Cloud. Used in Azure Cobalt 100, Alibaba Yitian 710.[^17] Product Page: [https://developer.arm.com/Processors/Neoverse%20N2%20Compute%20Subsystem][^16]                                                                                                     |
| SiFive   | Performance P870 / P870-D   | RISC-V (RV64GC, RVA23)                        | AP Core                  | 6-wide OoO, up to 32 cores (P870) / up to 256 cores (P870-D via CHI bridge), Shared Cluster Cache, RAS, IOMMU, WorldGuard                                                                | SPECint2k6/MHz: \~18.[^20] SPECint2k7/GHz: \>2.[^21] 50% perf uplift vs P670.[^20] Freq: \>3GHz target.[^20] CoreMark/DMIPS: N/A in sources.                                                                                                                 | Highest performance SiFive core. Target: Datacenter, AI, Mobile, Consumer, Edge Infrastructure. Product Page: [https://www.sifive.com/cores/performance-p870d][^21]                                                                                                                                                                            |
| SiFive   | Performance P670            | RISC-V (RV64GCV, RVA22)                       | AP Core                  | 4-issue OoO, 13-stage pipeline, up to 16 cores, Vector v1.0 (2x128b ALU), Vector Crypto, Private L2, ECC, Hypervisor Ext, WorldGuard                                                     | SPECint2k6/GHz: \>12.[^22] \>50% perf uplift vs P550.[^22] CoreMark/DMIPS: N/A in sources.                                                                                                                                                                   | Very high performance vector core. Target: Mobile, Consumer, Datacenter, Edge Infrastructure. Product Page: [https://www.sifive.com/cores/performance-p650-670][^22]                                                                                                                                                                           |
| SiFive   | Performance P550            | RISC-V (RV64GBC)                              | AP Core                  | 3-issue OoO, 13-stage pipeline, up to 4 cores, Sv39/Sv48 VM, Private L2, Prefetcher, ECC                                                                                                 | SPECint2k6/GHz: \>8.6.[^23] Higher single-thread perf vs Cortex-A75.[^23] CoreMark/DMIPS: N/A in sources. Geekbench 6 (HiFive Premier): SC: 136, MC: 423.[^24]                                                                                               | High performance core. Target: Mobile, Consumer, Datacenter, Edge Infrastructure. Used in HiFive Premier board @ 1.4GHz.[^25] Product Page: [https://www.sifive.com/cores/performance-p550][^23]                                                                                                                                               |
| Andes    | AX65                        | RISC-V (RV64GCBK, CMO, Andes ext.)            | AP Core                  | 13-stage OoO, 4-wide decode, 8 functional units, up to 8 cores, L1/L2 Cache (Opt. ECC), TAGE BP, MMU (Sv48), ePMP                                                                        | CoreMark/MHz: 9.25.[^26] DMIPS/MHz: 4.9.[^26] SPECint2006/GHz: 8.25.[^26] Freq: \>2.0GHz (12nm).[^27]                                                                                                                                                        | High performance OoO core. Target: Linux Apps, Computing, Networking, High-end Controllers, AI/ML main processor.[^26] [^27] Product Page: [https://www.andestech.com/en/products-solutions/andescore-processors/riscv-ax65/][^26]                                                                                                             |
| Andes    | AX46MPV                     | RISC-V (RV64GCBPV + Matrix, RVA22)            | AP Core                  | 8-stage dual-issue, up to 16 cores, Private L2, Shared L3, Vector (2048b VLEN), Matrix Ext, BF16, TrustZone-level security (ePMP/IOPMP), ACE_RVV                                         | CoreMark/MHz: \>6.3.[^28] DMIPS/MHz: \>3.9.[^28] SPECint2006/GHz: \>4.3.[^28] \>15% SPECint2006 uplift vs AX45MPV.[^29]                                                                                                                                      | High performance vector/matrix core. Target: Network Processors (Linux), High-perf Embedded, AI/ML.[^29] Availability Q1/Q2 2025.[^29] Product Page: N/A (Announced Oct 2024)                                                                                                                                                                  |
| Andes    | AX45MPV                     | RISC-V (RV64GCBPV, Andes ext.)                | AP Core                  | 8-stage dual-issue, up to 8 cores, L1/L2 Cache, VPU (up to 1024b VLEN/DLEN), MMU, PLIC, CoDense                                                                                          | CoreMark/MHz: 5.86.[^30] DMIPS/MHz: 3.39.[^30] SPECint: N/A in sources.                                                                                                                                                                                      | Vector core for Linux/RTOS. Target: ML/DL, Vision, DSP, Networking.[^30] Used in Renesas RZ/Five @ 1.0GHz.[^31] Product Page: [https://www.andestech.com/en/products-solutions/andescore-processors/riscv-ax45mpv/][^30]                                                                                                                       |
| Nuclei   | UX900                       | RISC-V (RV64IMACFDPBVK/Zc)                    | AP Core                  | 9-stage dual-issue, up to 16 cores SMP, MMU (Sv39/48), Opt. I/D Cache (16-64KB, ECC), Opt. Cluster Cache, FPU(DP), VPU, PMP, TEE                                                         | CoreMark/MHz: \~5.0 (Est. based on similar cores [^32] [^33]). DMIPS/MHz: \~2.9 (Est. based on similar cores [^33]). SPECint N/A in sources.                                                                                                                 | Linux-capable AP core. Target: 64b Linux, Application Processor, ADAS, Robotics.[^34] Product Page: [https://nucleisys.com/product/900.php][^34]                                                                                                                                                                                               |
| SpaceMIT | Key Stone K1 (X60 core)     | RISC-V (RV64GCVB, RVA22)                      | AP Core (Edge/AI)        | 8-core (4+4), 8-stage dual-issue in-order, 32KB L1 I/D, 512KB L2/cluster, 512KB TCM (AI cluster), 256b Vector (RVV 1.0), PMP/ePMP, Custom AI instr. [^35] [^36] [^37]                    | DMIPS: 50K total (8 cores).[^35] [^38] CoreMark/MHz: \~3.57 (per core, based on OpenBenchmarking total 45662 @ 8x1.6GHz). SPECint: N/A. Geekbench 5 SC:\~80-84, MC:\~334-514 @ 1.6GHz. Single core \~30% faster than A55.[^35] [^39] 2.0 TOPS AI.[^35] [^38] | Edge AI CPU. Target: SBC, NAS, Robots, Industrial, Edge.[^35] [^38] Used in Banana Pi BPI-F3, Bit-Brick K1.[^35] [^36] Product Page: [https://www.spacemit.com/en/key-stone-k1/][^40]. OpenBenchmarking: [https://openbenchmarking.org/result/2406158-NE-SPACEMITX17][^41]. Geekbench 5: [https://browser.geekbench.com/v5/cpu/22180854][^42]. |
| SpaceMIT | VitalStone V100 (X100 core) | RISC-V (RV64GCBV, RVA23)                      | AP Core (Server)         | Up to 64 cores, 12-stage 4-issue OoO, 256b Vector (RVV 1.0), Vector Crypto, Virtualization (H, AIA, IOMMU), RAS, Security (IOPMP, Side-channel prot.), BRS, 12nm [^43] [^44] [^45] [^46] | SPECint2k6/GHz: 7.5 [^45] (or \>9 [^46]). CoreMark/MHz: 7.7.[^45] DMIPS/MHz: 6.5.[^45] Single core perf \> A75.[^45] Freq: up to 2.5GHz.[^43] [^46]                                                                                                          | Server/Datacenter CPU. Target: Server, AI/ML, Edge Compute, Autonomous Driving.[^43] [^45] [^46] Product Page: N/A (Announced Jan 2025 [^44] [^46] [^47])                                                                                                                                                                                      |

_Note: Performance metrics like SPECint and CoreMark/DMIPS can vary significantly based on compiler flags, memory system, and specific core configuration. Stated values are typically vendor claims or estimates based on available data; refer to linked sources for context. N/A indicates data was not found in the provided sources or readily available verified external sources._

---

**Table 2: Microcontroller (MCU) Core Comparison**

| Vendor   | Product Model             | Architecture                   | Category                  | Key Configuration                                                                                                                                                                                           | Performance Metrics                                                                                                                        | Remarks                                                                                                                                                                                                                      |
| -------- | ------------------------- | ------------------------------ | ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ARM      | Cortex-M85                | Armv8.1-M Mainline             | MCU Core                  | 7-stage pipeline, Dual-issue (most instr), Opt. FPU (HP/SP/DP), Helium (MVE), Opt. I/D Cache (up to 64KB, ECC), Opt. TCM (up to 16MB, ECC), TrustZone, Opt. Custom Instructions (ACI), NVIC (up to 480 IRQ) | CoreMark/MHz: \>6.0.[^48] DMIPS/MHz: \>3.0 (Scalar, up to 8.76 claimed [^49]).[^48] [^49] SPECint: N/A.                                    | Highest performing Cortex-M. Target: High-perf IoT, Industrial, Automotive (ASIL D ready via DCLS/TFP/ECC/MBIST).[^48] [^50] Product Page: [https://developer.arm.com/Processors/Cortex-M85][^51]                            |
| ARM      | Cortex-M55                | Armv8.1-M Mainline             | MCU Core                  | 4-5 stage pipeline, Opt. FPU (SP/HP), Helium (MVE), Opt. I/D Cache (up to 64KB, ECC), Opt. TCM (up to 16MB, ECC), TrustZone, NVIC                                                                           | CoreMark/MHz: 4.2.[^52] DMIPS/MHz: 1.6.[^52] SPECint: N/A.                                                                                 | ML/DSP focused core. Target: Edge AI/ML, DSP applications.[^52] Product Page: [https://developer.arm.com/Processors/Cortex-M55][^53]                                                                                         |
| ARM      | Cortex-M33                | Armv8-M Mainline               | MCU Core                  | 3-stage pipeline, Opt. FPU (SP), Opt. DSP, TrustZone, Opt. MPU (up to 16 regions), AHB5, NVIC (up to 480 IRQ)                                                                                               | CoreMark/MHz: 4.02.[^52] DMIPS/MHz: 1.5.[^52] SPECint: N/A.                                                                                | Mainstream secure MCU core. Target: General Purpose MCU, IoT Security.[^52] Product Page: [https://developer.arm.com/Processors/Cortex-M33][^54]                                                                             |
| ARM      | Cortex-M0+                | Armv6-M                        | MCU Core                  | 2-stage pipeline, No FPU/DSP, Opt. MPU (8 regions), AHB-Lite, Von Neumann arch., NVIC (up to 32 IRQ)                                                                                                        | CoreMark/MHz: 2.46.[^52] DMIPS/MHz: 0.95.[^52] SPECint: N/A.                                                                               | Ultra-low power core. Target: 8/16-bit replacement, Simple controllers, Low power IoT.[^52] [^55] Product Page: [https://developer.arm.com/Processors/Cortex-M0+][^56]                                                       |
| SiFive   | Essential E76 / S76       | RISC-V (RV32IMAFC / RV64GC)    | MCU Core                  | 8-stage dual-issue pipeline, Opt. FPU (SP/DP/HP), Opt. ECC, Opt. Cache/TIM, Security Pkgs                                                                                                                   | CoreMark/MHz: 5.75.[^57] DMIPS/MHz: 3.32.[^57] SPECint: N/A.                                                                               | Highest performance Essential core. Target: High-perf real-time, Industrial, Edge Compute.[^57] Product Page: [https://www.sifive.com/cores/essential-7][^57]                                                                |
| SiFive   | Essential E6 / S6         | RISC-V (RV32IMAFC / RV64GC)    | MCU Core                  | 8-stage single-issue pipeline, Opt. FPU (SP/DP/HP), Opt. ECC, Opt. Cache/TIM, Security Pkgs                                                                                                                 | CoreMark/MHz: 3.8.[^58] DMIPS/MHz: 2.1.[^58] SPECint: N/A.                                                                                 | Mid-range performance core. Target: General purpose embedded, Industrial, IoT, Automotive.[^58] Product Page: [https://www.sifive.com/cores/essential-6][^58]                                                                |
| SiFive   | Essential E2 / S2         | RISC-V (RV32EMC / RV64IMC)     | MCU Core                  | 2-4 stage pipeline, Opt. FPU (SP/DP/HP), Bit manip ext, Opt. uICache/TIM, Security Pkgs                                                                                                                     | CoreMark/MHz: \~3.1 (E21/E24 [^32]). DMIPS/MHz: Up to 1.77.[^59] SPECint: N/A.                                                             | Smallest, most configurable core. Target: Ultra-low power, Area optimized, 8/32-bit replacement, PMIC, FSM.[^59] Product Page: [https://www.sifive.com/cores/essential-2][^59]                                               |
| Andes    | D23                       | RISC-V (RV32IMACBZceFDKP)      | MCU Core                  | 3-stage pipeline (single/dual issue), Opt. Cache, ECC, ePMP, sPMP, CMO, ACE support                                                                                                                         | CoreMark/MHz: 4.55.[^60] DMIPS/MHz: 2.08.[^60] SPECint: N/A.                                                                               | Compact core with DSP/FPU. Target: IoT, Embedded, Wearables, Sensors, Automotive/Industrial.[^60] Product Page: [https://www.andestech.com/en/products-solutions/andescore-processors/d23/][^61]                             |
| Andes    | N225                      | RISC-V (RV32IMACBZce)          | MCU Core                  | 3-stage pipeline (single/dual issue), ePMP                                                                                                                                                                  | CoreMark/MHz: 4.4.[^60] DMIPS/MHz: 1.92.[^60] SPECint: N/A.                                                                                | Compact, low-power core. Target: IoT, Embedded, Wearables, Sensors.[^60] Product Page: [https://www.andestech.com/en/products-solutions/andescore-processors/n225/][^62]                                                     |
| Andes    | D45-SE                    | RISC-V (RV32GCBP, Andes P-ext) | MCU Core                  | 8-stage dual-issue pipeline, FPU (SP/DP), DCLS, ECC, Bus Protection, StackSafe, Split-mode                                                                                                                  | CoreMark/MHz: 6.12.[^63] DMIPS/MHz: 2.96.[^64] SPECint: N/A.                                                                               | Functional Safety core. Target: Automotive ASIL-D applications.[^63] Product Page: [https://www.andestech.com/en/products-solutions/andescore-processors/d45-se/][^65]                                                       |
| Andes    | N22                       | RISC-V (RV32EMAC, Andes ext.)  | MCU Core                  | 2-stage pipeline                                                                                                                                                                                            | CoreMark/MHz: 3.95.[^60] DMIPS/MHz: 1.8.[^60] SPECint: N/A.                                                                                | Low-power, small core. Target: Deeply embedded.[^60] Product Page: [https://www.andestech.com/en/products-solutions/andescore-processors/n22/][^66]                                                                          |
| Nuclei   | N300 Series (e.g., N309)  | RISC-V (RV32IMACFDBPKC/Zc)     | MCU Core                  | 3-stage pipeline (Opt. Dual-issue), FPU (SP/DP), DSP (SIMD), Opt. Cache (ECC), Opt. ILM/DLM, TEE, NICE, ECLIC                                                                                               | CoreMark/MHz: N/A in sources. DMIPS/MHz: N/A in sources. SPECint: N/A.                                                                     | High efficiency core with DSP/FPU. Target: AIoT, Industrial Control, Smart Speaker, Wi-Fi/BLE.[^67] [^68] ASIL-D Ready (NA300D).[^69] Product Page: [https://nucleisys.com/product/300.php][^68]                             |
| Nuclei   | N200 Series (e.g., N205)  | RISC-V (RV32EMACB/Zc)          | MCU Core                  | 2-stage pipeline, Opt. ICache, Opt. ILM/DLM (N205), TEE, NICE, ECLIC                                                                                                                                        | CoreMark/MHz: \~3.33 (Inferred from GD32VF103 [^70]). DMIPS/MHz: N/A in sources. SPECint: N/A.                                             | Low power, area efficient core. Target: Deeply embedded, Secure elements.[^71] Used in GD32VF103, Amlogic Secure Proc.[^71] Product Page: [https://nucleisys.com/product/200.php][^71]                                       |
| Synopsys | ARC HS5x (e.g., HS56)     | ARCv3 (32-bit)                 | MCU Core                  | Dual-issue superscalar, L1 Cache, Opt. CCM, Opt. FPU                                                                                                                                                        | CoreMark/MHz: 6.16.[^72] DMIPS/MHz: 3.0.[^72] Freq: Up to 1.8GHz (16FFC).[^72] SPECint: N/A.                                               | High performance classic ARC core. Target: Real-time embedded.[^72] Product Page: [https://www.synopsys.com/dw/ipdir.php?ds=arc-hs5x-processors][^72]                                                                        |
| Synopsys | ARC EM Series (EM4/EM6)   | ARCv2 (32-bit)                 | MCU Core                  | Pipeline N/S, Opt. Cache (EM6), ICCM/DCCM, AHB/AHB-Lite                                                                                                                                                     | CoreMark/MHz: 4.18.[^73] DMIPS/MHz: 1.81.[^73] Area: 0.01mm² (28HPM).[^73] SPECint: N/A.                                                   | Ultra-low power, area-sensitive core. Target: Power/Area critical embedded.[^73] [^74] Product Page: [https://www.synopsys.com/dw/ipdir.php?ds=arc-em4-em6][^73]                                                             |
| Synopsys | ARC-V RMX-500(D)          | RISC-V (RV32)                  | MCU Core                  | 5-stage Harvard pipeline, Opt. L1 Cache (64KB), Opt. CCM (2MB), Opt. DSP (RMX-500D), Custom Instr, ECC/Parity, APLIC                                                                                        | CoreMark/MHz: N/A in sources. DMIPS/MHz: N/A in sources. SPECint: N/A.                                                                     | Power/Performance efficient RISC-V core. Target: Embedded, IoT Wearables (DSP).[^75] Product Page: [https://www.synopsys.com/dw/ipdir.php?ds=arc-v-rmx-500][^75]                                                             |
| Synopsys | ARC-V RHX-100(V) / 105(V) | RISC-V (RV32)                  | MCU Core                  | Dual-issue superscalar, up to 16 cores (105), Opt. Vector (RVV), Opt. MMU/L2 (105), Real-Time Trace                                                                                                         | CoreMark/MHz: N/A in sources. DMIPS/MHz: N/A in sources. SPECint: N/A.                                                                     | High performance real-time RISC-V core. Target: Real-time applications.[^76] RHX-110-FS targets ASIL D.[^76] Product Page: [https://www.synopsys.com/designware-ip/processor-solutions/arc-v-processors/arc-v-rhx.html][^76] |
| Cadence  | Tensilica Fusion F1       | Xtensa (Configurable)          | MCU Core (DSP)            | Dual-issue VLIW (HiFi 3 based), Flexible MAC, Opt. FPU (SP), Opt. Quad MAC, Opt. AES, Opt. Bit manip                                                                                                        | CoreMark/MHz: Up to 4.61.[^77] DMIPS/MHz: N/A in sources. SPECint: N/A.                                                                    | Ultra-low energy DSP/Controller. Target: IoT, Wearables, NB-IoT, Sensor Fusion, Always-on.[^77] [^78] Used in NXP i.MX RT500.[^79] Product Page: [https://www.design-reuse.com/sip/tensilica-fusion-f1-dsp-ip-45117/][^78]   |
| Cadence  | Tensilica HiFi 5          | Xtensa (Configurable)          | MCU Core (DSP)            | 5-slot VLIW, DSP (8x 32x32 MACs/cycle), NN Accel (32x 16x8 MACs/cycle), Opt. FPU (SP/HP), HiFi NN Lib                                                                                                       | CoreMark/MHz: N/A in sources. DMIPS/MHz: N/A in sources. SPECint: N/A.                                                                     | High performance AI/Audio DSP. Target: AI Speech/Audio, Voice Control, Automotive Infotainment (FuSa certified).[^80] [^81] Product Page: [https://www.design-reuse.com/sip/tensilica-hifi-5-dsp-ip-45673/][^82]             |
| Cadence  | Xtensa LX7                | Xtensa (Configurable)          | MCU Core (DSP/Controller) | Configurable 5/7 stage pipeline, Configurable FP (2-64 FLOPS/cycle), Opt. DSP blocks (Vision P6, Fusion G3, ConnX BBE), AXI, Opt. iDMA/MPU/ECC                                                              | CoreMark/MHz: N/A (Config dependent). DMIPS/MHz: N/A (Config dependent). (Older LX EEMBC scores high but dated [^83] [^84]). SPECint: N/A. | Highly configurable DSP/Controller platform.[^85] [^86] Target: Custom DSP/Controller applications. Product Page: N/A (Platform IP)                                                                                          |

_Note: Performance metrics like CoreMark/MHz and DMIPS/MHz can vary significantly based on compiler flags, memory system (Cache/TCM usage), and specific core configuration. Stated values are typically vendor claims or estimates based on available data; refer to linked sources for context. N/A indicates data was not found in the provided sources or readily available verified external sources._

## References


[^1]: [Cortex-A720 | Armv9.2 CPU with High Performance and Efficiency – Arm®](https://www.arm.com/products/silicon-ip-cpu/cortex-a/cortex-a720)

[^2]: [Latest ARM CPU cores compared: Performance-Per-Area and Performance-Per-Clock](https://www.reddit.com/r/hardware/comments/1gvo28c/latest_arm_cpu_cores_compared_performanceperarea/)

[^3]: [Cortex-A520 - Arm Developer](https://developer.arm.com/Processors/Cortex-A520)

[^4]: [sbc-bench/Benchmarking_some_benchmarks.md at master - GitHub](https://github.com/ThomasKaiser/sbc-bench/blob/master/Benchmarking_some_benchmarks.md)

[^5]: [developer.arm.com](https://developer.arm.com/-/media/Arm%20Developer%20Community/PDF/Cortex-A%20R%20M%20datasheets/Arm%20Cortex-M%20Comparison%20Table_v3.pdf)

[^6]: [ARM Cortex-A78 4 Core 1958 MHz - CPU Benchmarks](https://www.cpubenchmark.net/cpu.php?cpu=ARM+Cortex-A78+4+Core+1958+MHz&id=6589)

[^7]: [ARM Cortex-A78 4 Core 2000 MHz - CPU Benchmarks](https://www.cpubenchmark.net/cpu.php?cpu=ARM+Cortex-A78+4+Core+2000+MHz&id=5476)

[^8]: [Sustained performance through Arm Cortex-A78 CPU - Architectures and Processors blog](https://community.arm.com/arm-community-blogs/b/architectures-and-processors-blog/posts/arm-cortex-a78-cpu)

[^9]: [SPEC - Single Threaded Performance & Power - The Snapdragon 888 vs The Exynos 2100: Cortex-X1 & 5nm - Who Does It Better? - AnandTech](https://www.anandtech.com/show/16463/snapdragon-888-vs-exynos-2100-galaxy-s21-ultra/4)

[^10]: [Cortex-A78 - Arm Developer](https://developer.arm.com/Processors/Cortex-A78)

[^11]: [ARM Cortex-A55 8 Core 1800 MHz - CPU Benchmarks](https://www.cpubenchmark.net/cpu.php?cpu=ARM+Cortex-A55+8+Core+1800+MHz&id=5104)

[^12]: [ARM Cortex-A55 4 Core 2100 MHz - CPU Benchmarks](https://www.cpubenchmark.net/cpu.php?cpu=ARM+Cortex-A55+4+Core+2100+MHz&id=4555)

[^13]: [Cortex-A55 - Arm Developer](https://developer.arm.com/Processors/Cortex-A55)

[^14]: [Neoverse V3 | Enhanced Cloud & ML with Confidential Computing - Arm](https://www.arm.com/products/silicon-ip-cpu/neoverse/neoverse-v3)

[^15]: [Neoverse V3 - Arm Developer](https://developer.arm.com/Processors/Neoverse%20V3)

[^16]: [Neoverse N2 Compute Subsystem - Arm Developer](https://developer.arm.com/Processors/Neoverse%20N2%20Compute%20Subsystem)

[^17]: [ARM Neoverse - Wikipedia](https://en.wikipedia.org/wiki/ARM_Neoverse)

[^18]: [Neoverse N2 Reference Design - Arm Developer](https://developer.arm.com/Tools%20and%20Software/Neoverse%20N2%20Reference%20Design)

[^19]: [ARM Neoverse-N2 8 Core 2500 MHz - CPU Benchmarks](https://www.cpubenchmark.net/cpu.php?cpu=ARM+Neoverse-N2+8+Core+2500+MHz&id=6230)

[^20]: [SiFive Performance P870 and the SiFive Intelligence X390 - Jon Peddie Research](https://www.jonpeddie.com/news/sifive-performance-p870-and-the-sifive-intelligence-x390/)

[^21]: [SiFive Performance™ P870-D](https://www.sifive.com/cores/performance-p870d)

[^22]: [SiFive Performance™ P650/P670](https://www.sifive.com/cores/performance-p650-670)

[^23]: [SiFive Performance™ P550](https://www.sifive.com/cores/performance-p550)

[^24]: [SiFive HiFive Premier P550 Review: High RISC | Tom's Hardware](https://www.tomshardware.com/maker-stem/rp2040-boards/hifive-premier-p550-review)

[^25]: [HiFive Premier P550 - SiFive Boards](https://www.sifive.com/boards/hifive-premier-p550)

[^26]: [RISC-V: AX65 - Andes Technology](https://www.andestech.com/en/products-solutions/andescore-processors/riscv-ax65/)

[^27]: [Andes Announces General Availability of the New RISC-V Out-Of-Order Superscalar Multicore Processor, the AndesCore AX65 - HPCwire](https://www.hpcwire.com/off-the-wire/andes-announces-general-availability-of-the-new-risc-v-out-of-order-superscalar-multicore-processor-the-andescore-ax65/)

[^28]: [RISC-V: AX46MPV - Andes Technology](https://www.andestech.com/en/products-solutions/andescore-processors/riscv-ax46mpv/)

[^29]: [Andes Announces the AndesCore™ 46-Series ... - GlobeNewswire](https://www.globenewswire.com/news-release/2024/10/21/2966340/0/en/Andes-Announces-the-AndesCore-46-Series-Family-and-the-3rd-generation-Vector-Processor-AX46MPV-with-Matrix-Extension.html)

[^30]: [RISC-V: AX45MPV - Andes Technology](https://www.andestech.com/en/products-solutions/andescore-processors/riscv-ax45mpv/)

[^31]: [RZ/Five - General-purpose Microprocessors with RISC-V CPU Core (Andes AX45MP Single) (1.0 GHz) with 2ch Gigabit Ethernet | Renesas](https://www.renesas.com/en/products/microcontrollers-microprocessors/rz-mpus/rzfive-general-purpose-microprocessors-risc-v-cpu-core-andes-ax45mp-single-10-ghz-2ch-gigabit-ethernet)

[^32]: [CoreMark/MHz - WikiChip](https://en.wikichip.org/wiki/coremark-mhz)

[^33]: [Performance and Area — NaxRiscv documentation - GitHub Pages](https://spinalhdl.github.io/NaxRiscv-Rtd/main/NaxRiscv/performance/index.html)

[^34]: [900 Series 32-Bit/64-bit processor_Nuclei-Best RISC-V Processor IP - Nuclei System](https://nucleisys.com/product/900.php)

[^35]: [SpacemiT K1 8 core RISC-V chip Brief - BananaPi Docs](https://docs.banana-pi.org/en/BPI-F3/SpacemiT_K1)

[^36]: [SpacemiT X60 RISC V Processor Enables AI and High Speed Storage in Bit Brick K1 Embedded Board - LinuxGizmos.com](https://linuxgizmos.com/spacemit-x60-risc-v-processor-enables-ai-and-high-speed-storage-in-bit-brick-k1-embedded-board/)

[^37]: [Banana Pi BPI-F3 SpacemiT K1 RISC-V chip datasheet | BananaPi Docs](https://docs.banana-pi.org/en/BPI-F3/SpacemiT_K1_datasheet)

[^38]: [SpacemiT Products Make a Splash at the 2024 RISC-V North America Summit](https://www.spacemit.com/en/news/spacemit-products-make-a-splash-at-the-2024-risc-v-north-america-summit/)

[^39]: [What's the Current Performance Level of the Most Powerful RISC-V Cores? - Reddit](https://www.reddit.com/r/RISCV/comments/1coxdwm/whats_the_current_performance_level_of_the_most/)

[^40]: [SpacemiT Key Stone](https://www.spacemit.com/en/key-stone-k1/)

[^41]: [OpenBenchmarking: 2406158-NE-SPACEMITX17](https://openbenchmarking.org/result/2406158-NE-SPACEMITX17)

[^42]: [Geekbench 5: 22180854](https://browser.geekbench.com/v5/cpu/22180854)

[^43]: [China's SpacemiT develops 64-core RISC-V datacenter CPU — 12nm chip allegedly performs like a 10-year old Xen or Opteron but with higher core count | Tom's Hardware](https://www.tomshardware.com/pc-components/cpus/chinas-spacemit-develops-64-core-risc-v-datacenter-cpu-12nm-chip-allegedly-performs-like-a-10-year-old-xen-or-opteron-but-with-higher-core-count)

[^44]: [RISC-V Breakthrough: SpacemiT Develops Server CPU Chip V100 for Next-Generation AI Applications - PR Newswire](https://www.prnewswire.com/ru/press-releases/risc-v-breakthrough-spacemit-develops-server-cpu-chip-v100-for-next-generation-ai-applications-302343637.html)

[^45]: [SpacemiT makes important breakthroughs in RISC-V High-Performance Cores!](https://www.spacemit.com/en/news/spacemit-makes-important-breakthroughs-in-risc-v-high-performance-cores/)

[^46]: [RISC-V Breakthrough: SpacemiT Develops Server CPU Chip V100 for Next-Gen AI Applications | TechPowerUp](https://www.techpowerup.com/330849/risc-v-breakthrough-spacemit-develops-server-cpu-chip-v100-for-next-gen-ai-applications)

[^47]: [SpacemiT - RISC-V SoC](https://www.spacemit.com/en/)

[^48]: [Cortex-M85: Safety and performance updates - Internet of Things (IoT) blog](https://community.arm.com/arm-community-blogs/b/internet-of-things-blog/posts/cortex-m85-safety-and-performance-updates)

[^49]: [Arm Cortex-M85 is faster than Cortex-M7, offers higher ML performance than Cortex-M55 - CNX Software](https://www.cnx-software.com/2022/04/27/arm-cortex-m85-is-faster-than-cortex-m7-offers-higher-ml-performance-than-cortex-m55/)

[^50]: [About the Cortex-M85 processor and core peripherals - Arm Developer](https://developer.arm.com/documentation/101928/0101/Overview--Reference-Material/About-the-Cortex-M85-processor-and-core-peripherals)

[^51]: [Cortex-M85 - Arm Developer](https://developer.arm.com/Processors/Cortex-M85)

[^52]: [Arm Cortex-M Comparison Table](https://developer.arm.com/-/media/Arm%20Developer%20Community/PDF/Cortex-A%20R%20M%20datasheets/Arm%20Cortex-M%20Comparison%20Table_v3.pdf)

[^53]: [Cortex-M55 - Arm Developer](https://developer.arm.com/Processors/Cortex-M55)

[^54]: [Cortex-M33 - Arm Developer](https://developer.arm.com/Processors/Cortex-M33)

[^55]: [Cortex-M0 - Arm Developer](https://developer.arm.com/Processors/Cortex-M0)

[^56]: [Cortex-M0+ - Arm Developer](https://developer.arm.com/Processors/Cortex-M0+)

[^57]: [SiFive Essential™ 7-Series](https://www.sifive.com/cores/essential-7)

[^58]: [SiFive Essential™ 6-Series](https://www.sifive.com/cores/essential-6)

[^59]: [SiFive Essential™ 2-Series](https://www.sifive.com/cores/essential-2)

[^60]: [Andes Technology Unveils Andes D23 and N225 Cores Pioneering ...](https://www.design-reuse.com/news/55026/andes-risc-v-d23-n225-processor-cores.html)

[^61]: [RISC-V: D23 - Andes Technology](https://www.andestech.com/en/products-solutions/andescore-processors/d23/)

[^62]: [RISC-V: N225 - Andes Technology](https://www.andestech.com/en/products-solutions/andescore-processors/n225/)

[^63]: [Andes Technology Unveils the D45-SE RISC-V ... - GlobeNewswire](https://www.globenewswire.com/news-release/2024/10/22/2967137/0/en/Andes-Technology-Unveils-the-D45-SE-RISC-V-Processor-Targeting-ASIL-D-Certification.html)

[^64]: [RISC-V: D45-SE - Andes Technology](https://www.andestech.com/en/products-solutions/andescore-processors/riscv-d45-se/)

[^65]: [RISC-V: D45-SE - Andes Technology](https://www.andestech.com/en/products-solutions/andescore-processors/d45-se/)

[^66]: [RISC-V: N22 - Andes Technology](https://www.andestech.com/en/products-solutions/andescore-processors/n22/)

[^67]: [Nuclei RISC-V 300 Series Processors](https://www.riscvschool.com/2023/02/18/nuclei-risc-v-300-series-processors/)

[^68]: [N300 Series 32-Bit risc-v processor_Nuclei-Best RISC-V Processor IP - Nuclei System](https://nucleisys.com/product/300.php)

[^69]: [Nuclei, the World's First RISC-V CPU IP Vendor to Accomplish ISO 26262 ASIL-D Product Certificate - EE Times](https://www.eetimes.com/nuclei-the-worlds-first-risc-v-cpu-ip-vendor-to-accomplish-iso-26262-asil-d-product-certificate/)

[^70]: [Commercially available RISC-V silicon - Muxup](https://muxup.com/2023q1/commercially-available-risc-v-silicon)

[^71]: [N200 Series 32-Bit risc-v processor_Nuclei-Best RISC-V Processor IP - Nuclei System](https://www.nucleisys.com/product/200.php)

[^72]: [Synopsys ARC HS56, HS57D, and HS58 Processors](https://www.synopsys.com/dw/ipdir.php?ds=arc-hs5x-processors)

[^73]: [Ultra-low power ARC EM4 and EM6 processors - Synopsys](https://www.synopsys.com/dw/ipdir.php?ds=arc-em4-em6)

[^74]: [ARC Classic Processors | Synopsys](https://www.synopsys.com/designware-ip/processor-solutions/arc-classic-processors.html)

[^75]: [Synopsys ARC-V RMX-500 Processor IP](https://www.synopsys.com/dw/ipdir.php?ds=arc-v-rmx-500)

[^76]: [Synopsys ARC-V RHX Processor Series](https://www.synopsys.com/designware-ip/processor-solutions/arc-v-processors/arc-v-rhx.html)

[^77]: [Low Cost Power NB-IoT Solution? Fusion F1 DSP based Modem! - SemiWiki](https://semiwiki.com/eda/cadence/7624-low-cost-power-nb-iot-solution-fusion-f1-dsp-based-modem/)

[^78]: [Tensilica Fusion F1 DSP IP Core - Design And Reuse](https://www.design-reuse.com/sip/tensilica-fusion-f1-dsp-ip-45117/)

[^79]: [Using i.MX RT500 FusionF1 DSP in Low-Power - NXP Semiconductors](https://www.nxp.com/docs/en/application-note/AN13657.pdf)

[^80]: [Cadence Tensilica HiFi 5 DSPs Used in NXP's Next-Gen Audio DSP Family | SemiWiki](https://semiwiki.com/forum/threads/cadence-tensilica-hifi-5-dsps-used-in-nxp%E2%80%99s-next-gen-audio-dsp-family.21028/)

[^81]: [Cadence Introduces the Tensilica HiFi 5 DSP, the First DSP Optimized for AI Speech and Audio Processing - Design And Reuse](https://www.design-reuse.com/news/45056/cadence-tensilica-hifi-5-dsp-ai-speech-audio-processing.html)

[^82]: [Tensilica HiFi 5 DSP IP Core - Design And Reuse](https://www.design-reuse.com/sip/tensilica-hifi-5-dsp-ip-45673/)

[^83]: [Tensilica's Xtensa LX Processor Beats All Other 32- and 64-bit Processor Cores On EEMBC Consumer "Out of the Box" Benchmark - Design And Reuse](https://www.design-reuse.com/news/7870/tensilica-xtensa-lx-processor-beats-all-other-32-64-bit-processor-cores-eembc-consumer-box-benchmark.html)

[^84]: [Tensilica Xtensa LX Processor Beats All Other Processors and Cores On EEMBC Networking 2.0 and Office Automation Benchmarks - Design And Reuse](https://www.design-reuse.com/news/10371/tensilica-xtensa-lx-processor-beats-all-other-processors-cores-eembc-networking-2-0-office-automation-benchmarks.html)

[^85]: [Mirabilis Design Accelerates SoC Development with New System-Level IP Library for Cadence Tensilica Processors](https://www.design-reuse-embedded.com/news/202502110/mirabilis-design-accelerates-soc-development-with-new-system-level-ip-library-for-cadence-tensilica-processors/?lang=en)

[^86]: [Tensilica Xtensa LX7 processor architecture - Electronic Specifier](https://www.electronicspecifier.com/products/design-automation/tensilica-xtensa-lx7-processor-architecture)
