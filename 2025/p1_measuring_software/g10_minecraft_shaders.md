| Author | Title | Image | Date | Summary |
|--------|-------|-------|------|---------|
| Andrea,Ayush Kuruvilla,Sahar Marossi,Yulin Chen | **Minecraft Energy Consumption Comparison with and without Shaders** | ![Cover](../img/p1_measuring_software/gX_template/cover.png) | 28/02/2025 | This article presents a roadmap on how to properly set up a scientific methodology to measure energy consumption in Minecraft with and without shaders. We outline unbiased energy measurement strategies, discuss methodology and replication, and analyze results to draw meaningful conclusions about energy efficiency. |



## Problem Statement

Measuring energy consumption in gaming applications is a challenging task, especially when comparing different graphical settings. Minecraft is a widely popular game that allows extensive graphical modifications, including shader packs that enhance visual fidelity but may significantly impact power consumption.

This article focuses on comparing the energy consumption of Minecraft when running with and without shaders. Our goal is to measure how much additional power is required to render advanced lighting effects and reflections provided by shader packs and to discuss the implications for gamers and developers aiming for energy efficiency.

## Methodology

The experiment follows a structured process to measure energy consumption with minimal bias. The methodology includes:

- **Warmup Phase:** A Fibonacci sequence warmup function (`warmup.fibonacci_warmup()`) is executed before starting the experiment to ensure system stability and prevent initial spikes in energy consumption.
- **Iteration-Based Execution:** The experiment consists of 30 iterations per condition (with shaders and without shaders), shuffled randomly to minimize potential external influences.
- **Automated Execution:** Each test instance is run using a subprocess command with `energibridge`, ensuring consistent logging of GPU and CPU energy consumption.
- **Output Logging:** Each test generates an output CSV file containing detailed energy consumption data.
- **Resting Periods:** A 20-second rest period is included between each iteration to prevent thermal throttling and ensure consistency.

Experiment (Per Iteration)
Open Minecraft Launcher (10 seconds).
Launch the game (30 seconds).
Navigate and load the world (10 seconds).
Run player experiment (~40 seconds).
Buffer time (5 seconds). Load shaders if enabled.
Teleport player to start location. Set time to day (for lighting).
Walk forward for ~30 seconds through the map (designed to benchmark shader-lighting).
Disable shaders if enabled.
Close game via Alt-F4.
Rest for 60 seconds.
Total experiment time(Per Iteration) averages ~90 seconds.

## Setup

### Hardware Specifications:
- **Processor:** Intel(R) Core(TM) i7-9750H CPU @ 2.60GHz
- **GPU:** NVIDIA Quadro P2000
- **Installed RAM:** 16.0 GB (15.8 GB usable)
- **Monitor Refresh Rate:** 60Hz
- **Desktop Resolution:** 1920 x 1080
- **Color Format:** RGB
- **Color Space:** Standard Dynamic Range (SDR)

### Software Setup:
- **Minecraft Version:** 1.21.4
- **Modded Instance:** Iris-Fabric-1.8.8+MC1.21.4
- **Shaderpack:** Complementary Shaders 4.7.2
- **World File:** Lighting World (TODO: Share file)

## Replication

To ensure the experiment is replicable:
- The **same hardware and software settings** must be maintained across all runs.
- The **game world must be identical** for all test iterations.
- **All background processes and unnecessary peripherals must be disabled** to minimize external factors affecting energy consumption.
- The **GPU power should be logged at fixed intervals** (e.g., 2 seconds after execution and at peak load).

To replicate the experiment, the code for measuring energy consumption in Minecraft on Windows can be found in the **Energy Consumption** repository: [GitHub Link](https://github.com/Ayushkuruvilla/Energy_consumption).

## Results

We will compare the power consumption values collected from running Minecraft with and without shaders. Data will be presented in tabular and graphical formats to highlight differences in energy usage.
### Results averaged over 30 runs
|                    | Shaders Disabled  | Shaders Enabled  | Relative difference (mean) | t-test p-value |
|:-------------------|:-----------------:|:----------------:|:--------------------------:|:--------------:|
| Execution Time (s) |      65.336       |      65.488      |           +0.23%           |   1.538e-08    |
| CPU Energy (J)     |      533.224      |     752.289      |          +41.08%           |   3.583e-26    |
| CPU Power (W)      |       8.161       |      11.487      |          +40.76%           |   3.217e-26    |
| GPU Temp (°C)      |       55.76       |      58.20       |           +4.38%           |      0.0       |

### Results from median of 30 runs
|                    | Shaders Disabled | Shaders Enabled | Relative difference (mean) | t-test p-value |
|:-------------------|:----------------:|:---------------:|:--------------------------:|:--------------:|
| Execution Time (s) |      65.264      |     65.463      |           +0.30%           |   1.538e-08    |
| CPU Energy (J)     |     515.039      |     741.409     |          +43.95%           |   3.583e-26    |
| CPU Power (W)      |      7.881       |     11.310      |          +43.52%           |   3.217e-26    |
| GPU Temp (°C)      |      56.000      |     59.000      |           +5.36%           |      0.0       |

Running Minecraft with shaders significantly increases energy consumption and power usage while only slightly affecting execution time.
- **Time**: Minimal impact, with only a 0.23% increase in mean execution time and a 0.30% increase in median time when using shaders. The p-value suggests a statistically significant difference, but the effect size is negligible.
- **Energy**: Shaders caused a 41.08% increase in mean energy consumption and a 43.95% increase in median energy consumption, indicating a substantial rise in power demand.
- **Power**: The mean power usage rose by 40.76%, and the median power usage increases by 43.52%, reinforcing the conclusion that shaders place a significantly higher load on the system.
- **GPU Temperature**: The average GPU temperature rose by approximately 4-5%, confirming that shaders increase the thermal load, although the system’s cooling mechanism appears to handle the added heat efficiently.

While shaders have little effect on performance, they drastically increase resource consumption. The extremely low t-test p-values across all metrics confirm that these differences are statistically significant, making shaders costly in terms of power and energy efficiency.
| Shader Runs | No Shader Runs |
|------------|--------------|
| ![Shader Runs](/img/p1_measuring_software/gX_template/gpu_1.png) |(/img/p1_measuring_software/gX_template/gpu 2.1.png)
## Discussion
The results from the experiment suggest a noticeable trade-off between graphics quality and energy consumption for Minecraft. Although we observed that adding shader packs only increased the execution time by less than 1%, the additional power required to run the game is much more substantial. In particular, running Minecraft with shaders draws nearly 50% more power and the statistical significance derived from the t-test aligns with this observation. This was to be expected since introducing shaders adds additional overhead/load as the CPU manages the compilation and transfer of shader-related data between the GPU and the rest of the computer at runtime [^shaderanalysis]. 

This discrepancy highlights an issue for the gaming community as a whole. While the environmental and financial implications of increased energy consumption may not be too noticeable at a personal level, the additional energy demand and emissions produced are remarkable for a game with over 200 million monthly active players. 

Considering this, gamers should be more conscious of the economic and environmental impact of shader packs. Moreover, developing more computationally efficient shaders and optimizing the game around them would reduce Minecraft’s global environmental footprint while still delivering quality aesthetics for players worldwide.


## Limitations

- Energy measurements depend on system conditions and may vary slightly.
- Different shader packs may lead to different power consumption profiles.
- This experiment does not account for extended gameplay and only considers a limited test duration.

## Conclusion

This study provides an empirical analysis of the energy consumption differences in Minecraft with and without shaders. Our findings highlight the potential trade-offs between visual fidelity and power efficiency, offering insights for gamers and developers seeking optimized performance and sustainability.

By following proper scientific measurement techniques, we ensure that our results remain valid and reproducible. This ultimately contributes to better energy efficiency practices in gaming and software development.




