---
layout: default
---

## Subframe Preselection with Siril

### Selection Parameters: Background, FWHM, and Quality

This tutorial demonstrates how to filter your subframes to achieve a higher-quality stack. A prerequisite is a registered sequence (e.g., created via the `OSC_Preprocessing.ssf` script).

First, set Siril's working directory to your sequence location (typically the `process` folder). Navigate to the **Sequence** tab and click **Search Sequences**:

![Search Sequence](/Users/sven/Documents/Repositories/Trickx.github.io/images/siril/SearchSequence.png)

Open your sequence of registered light frames:

![Open Sequence](/Users/sven/Documents/Repositories/Trickx.github.io/images/siril/OpenSequence.png)

### Analyzing the Data

Head over to the **Plot** tab to analyze the quality of your frames. It is recommended to use **Autostretch** view to visually inspect the frames while browsing the data. 

First, let's examine the **FWHM** (Full Width at Half Maximum) values per frame. This metric indicates star sharpness:

![FWHM Plot](/Users/sven/Documents/Repositories/Trickx.github.io/images/siril/FWHMPlot.png)

The animation below illustrates the visual difference between a "bad" frame (bloated stars) and a "good" frame (sharp stars):

![FWHM Animation](/Users/sven/Documents/Repositories/Trickx.github.io/images/siril/FWHMAnimation.gif)

Similarly, we can inspect **Star Roundness** to identify frames with tracking issues or wind shakes:

![Roundness Animation](/Users/sven/Documents/Repositories/Trickx.github.io/images/siril/RoundnessAnimation.gif)

Finally, the **Background** level can be used to filter out frames affected by passing clouds, moonlight, or increasing light pollution:

![Background Animation](/Users/sven/Documents/Repositories/Trickx.github.io/images/siril/BackgroundAnimation.gif)

### Does Preselection Matter?

To evaluate the impact of filtering, we compare the following metrics:


| Metric        | Expectation                                     |
|---------------|-------------------------------------------------|
| **FWHM**      | Lower is better (sharper details).             |
| **Roundness** | Closer to 1.0 is better (perfect circles).     |
| **Background**| Lower is better (higher contrast).             |
| **SNR**       | Higher is better (less noise).                 |

By running a **Dynamic PSF** analysis on both the full stack and the filtered selection, we can quantify the improvements.

![Dynamic PSF](/Users/sven/Documents/Repositories/Trickx.github.io/images/siril/DynamicPSF.png)

### Results & Comparison


| Parameter | Full Stack | Selection | Observation & Impact |
|:----------|:-----------|:----------|:---------------------|
| **L** (No. of Frames)| 195 | 133 | Number of integrated light frames. |
| **N** (No. of Stars) | 5389 | 5557 | **Higher count:** Better SNR and sharpness allow for detecting fainter stars despite fewer frames. |
| **B** (Backgr.)| 0.009034 | 0.005775 | **Effectively reduced:** Lower background leads to significantly better contrast. |
| **A** (Amplitude)| 0.058814 | 0.066946 | **Increased:** Stars stand out more clearly against the noise floor. |
| **FWHM x/y** | 4.35" / 3.88" | 4.24" / 3.80" | **Improved:** Resulting in a crisper image with finer details. |
| **r** (Roundness)| 0.891 | 0.895 | **Improved:** Stars are closer to being perfect circles. |

**Conclusion on SNR:**
Since the **Amplitude (Signal)** increased while the **Background (Noise floor)** decreased, the overall **Signal-to-Noise Ratio (SNR)** has significantly improved in the filtered stack, even with 30% fewer frames.

[back](./)
