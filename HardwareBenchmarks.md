## Hardware benchmarks

This page can be used as a reference page for comparative performance benchmarks against OCI shapes

1. **Comparative benchmark Test - 1**
   * **Functional:** 2D tissue model simulations with 500 x 500 cells
   * **On-campus hardware:** Silicon Mechanics Blade Center with 8 x NVIDIA Tesla P100 + 8 x Intel(R) Xeon(R) Platinum 8160 CPU
2x NVIDIA Tesla P100-PCIE-16GB 2 x Intel(R) Xeon(R) Platinum 8160 CPU @ 2.10GHz (24 cores each = 48 cores in total)
   * **OCI shape:** VM.GPU3.2 2x NVIDIA V100 Tensor Core Intel(R) Xeon(R) Platinum 8167M CPU @ 2.00GHz, 12 cores (out of 26 physical cores)
   * [Processor comparison](https://www.cpu-world.com/Compare/759/Intel_Xeon_8160_vs_Intel_Xeon_8167M.html)
     * Key points: 8167M has more cores + (turbo enabled by default on OCI) for better multi-threading performance, handles more simultaneous threads
   
2. **Comparative benchmark Test - 2**
   * **Functional:** Molecular modeling with NAMD simulations
   * **on-campus hardware:** 8 x NVIDIA Tesla P100 + 8 x Intel(R) Xeon(R) Platinum 8160 CPU. Using 2 blade nodes, i.e.:
2x NVIDIA Tesla P100-PCIE-16GB 2 x Intel(R) Xeon(R) Platinum 8160 CPU @ 2.10GHz (24 cores each = 48 cores in total)
   * **OCI shape:** Oracle VM.GPU3.2 2x NVIDIA V100 Tensor Core Intel(R) Xeon(R) Platinum 8167M CPU @ 2.00GHz, 12 cores (out of 26 physical cores)
   * [Processor comparison](https://gadgetversus.com/processor/dual-intel-xeon-e5-2690-vs-intel-xeon-platinum-8167m/)
     * 8167M has more core power and in single core, the difference is 46% gain. In multi-core, the difference in terms of gap is 35% gain.
     * It is possible that processing power gain can be eliminated by comparing against VM vs BM shapes
