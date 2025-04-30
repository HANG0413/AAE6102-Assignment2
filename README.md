# AAE6102-Assignment2


## Overview

This project involves Assignment 2 for AAE6102: Satellite Communication and Navigation. The customized SDR is based on the open-source MATLAB code published by Bing Xu and Li-Ta Hsu [1].This project contains the following components:  
- `geo/` and `acqtckpos/` - Original source folders.  
- Multiple `.m` files for GNSS signal processing.  
- Two data files: `Urban` and `Opensky.bin`.  
- `SDR_main.m` - The main function for processing IF data.

## Table of Contents

- [Task 1 – Differential GNSS Positioning](#task-1--differential-gnss-positioning)
- [Task 2 – GNSS in Urban Areas](#task-2--gnss-in-urban-areas-with-skymask)
- [Task 3 – GPS RAIM (Receiver Autonomous Integrity Monitoring)](#task-3--raim-receiver-autonomous-integrity-monitoring)
- [Task 4 – LEO Satellites for Navigation](#task-4--leo-satellites-for-navigation)
- [Task 5 – GNSS Remote Sensing](#task-5--gnss-remote-sensing-via-gnss-ro)
- [References](#references)

## 🛠️  Task 1 – Differential GNSS Positioning

**Model:** ChatGPT 4o  
**Prompt:**  
Compose a short essay (500–1000 words) comparing the pros and cons of the following GNSS techniques for smartphone navigation:

- Differential GNSS (DGNSS)  
- Real-Time Kinematic (RTK)  
- Precise Point Positioning (PPP)  
- PPP-RTK

Smartphone navigation has become an essential component of daily life, powering applications ranging from ride-sharing to augmented reality. However, Global Navigation Satellite System (GNSS) measurements on smartphones are challenged by noise, multipath effects, and limited antenna quality, leading to relatively low positioning accuracy compared to dedicated GNSS receivers. To bridge this gap, advanced GNSS techniques such as Differential GNSS (DGNSS), Real-Time Kinematic (RTK), Precise Point Positioning (PPP), and PPP-RTK have been explored. Each method offers distinct advantages and faces particular challenges when applied to smartphones. This essay compares the pros and cons of these four techniques in the context of smartphone navigation.

## 🛰 Differential GNSS (DGNSS)
DGNSS enhances positioning accuracy by correcting satellite-related errors (e.g., atmospheric delays, clock errors) using data from nearby reference stations. Corrections are broadcast in real time, allowing the receiver to improve its position estimate.

**Pros:**
- ✅ Improved accuracy: DGNSS can reduce errors to the sub-meter level, significantly better than standalone GNSS, which typically has 3–10 meters of error on smartphones.
- ✅ Mature infrastructure: Many countries maintain DGNSS networks, and many smartphones are compatible with DGNSS corrections through assisted-GNSS (A-GNSS).
- ✅ Low cost: It is relatively inexpensive to access corrections, often provided free or at a low subscription fee.

**Cons:**
- ❌ Limited accuracy: Although DGNSS improves basic GNSS, its precision (~0.5–2 meters) is insufficient for applications requiring centimeter-level accuracy, such as lane-level navigation.
- ❌ Dependence on proximity: Corrections are most effective within about 100 km of the reference station. Accuracy degrades with distance.

## 🛰 Real-Time Kinematic (RTK)
RTK uses carrier-phase measurements rather than code pseudoranges to achieve centimeter-level positioning accuracy. A rover (smartphone) receives real-time corrections from a base station or network of base stations.
**Pros:**
- ✅ Centimeter-level accuracy: RTK can achieve ~1–5 cm positioning, opening up possibilities for high-precision smartphone applications like advanced augmented reality and autonomous driving.
Rapid convergence: Once initialized, RTK solutions can converge in seconds.

**Cons:**
- ❌ Infrastructure demands: RTK requires access to a dense network of base stations or a nearby local station, which may not be available in all regions.
- ❌ Communication needs: It depends on stable, low-latency communication (e.g., via cellular networks) to receive real-time corrections.
- ❌ Smartphone hardware limitations: RTK requires high-quality carrier-phase data. Most smartphones struggle with signal continuity and phase noise due to inferior antenna designs, making RTK less reliable unless specialized smartphones (e.g., those supporting dual-frequency GNSS) are used.
- ❌ Susceptibility to cycle slips: Smartphone movements and multipath can easily cause RTK solutions to break, requiring reinitialization.

## 🛰 Precise Point Positioning (PPP)
PPP is a global technique that applies precise satellite orbit and clock corrections to eliminate most GNSS errors without needing a nearby base station.

**Pros:**
- ✅ Global availability: PPP corrections are satellite-based or internet-delivered and work anywhere on Earth without needing a local network.
- ✅ No base stations required: This reduces infrastructure and communication costs significantly.
- ✅ Improved smartphone viability: PPP can function even with noisier smartphone GNSS signals, though with reduced accuracy compared to professional-grade receivers.
  
**Cons:**
Long convergence times: Traditional PPP solutions can take up to 30 minutes to converge to high accuracy, unsuitable for dynamic smartphone users who expect near-instant results.
Lower accuracy: PPP on smartphones typically achieves decimeter to sub-meter accuracy, better than standard GNSS but worse than RTK.

## 🛰 PPP-RTK
PPP-RTK combines the advantages of PPP and RTK: it uses precise satellite corrections like PPP but also leverages local corrections for faster convergence and higher accuracy.

**Pros:**
- ✅ Fast convergence: Compared to PPP alone, PPP-RTK reduces convergence times to seconds or a few minutes.
- ✅ Centimeter to decimeter accuracy: PPP-RTK can offer RTK-like accuracy without being as sensitive to infrastructure availability.
- ✅ Better resilience: It is more tolerant to signal interruptions and phase noise, which are major issues for smartphones.
- ✅ Broader applicability: It extends high-precision services even to remote areas where dense RTK networks are unavailable.
  
**Cons:**
- ❌ Still requires corrections: PPP-RTK needs access to satellite and atmospheric corrections through subscription services, which may add to costs.
- ❌ Dependence on service providers: Unlike pure PPP, PPP-RTK depends on correction networks that are typically commercial (e.g., Trimble, u-blox, or regional services).
Variable smartphone support: Full PPP-RTK functionality may still demand dual-frequency, carrier-phase capable smartphones, which are becoming available but not yet universal.

## Conclusion
Each GNSS enhancement technique brings a unique tradeoff between accuracy, availability, and practicality for smartphones.

**DGNSS** offers modest improvements at low cost but limited precision.

**RTK** provides superior accuracy but demands ideal conditions and high-end smartphone hardware.

**PPP** ensures global coverage but suffers from long convergence times.

**PPP-RTK** appears to strike the best balance, offering near-RTK performance with better resilience and global usability, although at the cost of needing commercial correction services and high-end smartphone capabilities.

For most everyday smartphone navigation applications, DGNSS or PPP provides a good balance of improvement and cost. However, for future high-precision use cases like autonomous vehicles, drone control, or precise AR experiences, PPP-RTK supported by new generation smartphones may become the dominant solution.
## 📊 Technique Comparison Table

| Technique   | Pros                                                                                                                                   | Cons                                                                                                                             | Typical Accuracy | Infrastructure Need                             | Suitability for Smartphones                                |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|------------------|--------------------------------------------------|------------------------------------------------------------|
| **DGNSS**   | - Improves basic GNSS accuracy  <br> - Widely available  <br> - Low cost                                                               | - Limited to sub-meter precision  <br> - Accuracy degrades with distance from base station                                      | ~0.5–2 meters    | Local DGNSS station network                     | Good for general smartphone navigation                    |
| **RTK**     | - Centimeter-level precision  <br> - Fast convergence once initialized                                                                | - Requires dense base stations  <br> - Needs stable communication  <br> - Sensitive to signal loss and cycle slips             | ~1–5 cm          | Nearby base station(s) + real-time communication | Challenging (requires dual-frequency, high-end smartphones) |
| **PPP**     | - Global coverage  <br> - No need for local infrastructure  <br> - Tolerant to moderate signal quality                                | - Long convergence time (minutes)  <br> - Slightly lower precision                                                              | ~0.2–1 meter     | Internet or satellite correction service        | Moderate (better with dual-frequency smartphones)          |
| **PPP-RTK** | - Combines PPP global reach with RTK speed  <br> - Fast convergence  <br> - Centimeter to decimeter accuracy  <br> - More resilient     | - Requires correction services (subscription)  <br> - Infrastructure lighter than RTK but still needed                         | ~5–20 cm         | Global correction network (commercial or regional) | Best with advanced smartphones (e.g., dual-frequency GNSS phones) |

## 🛠️ Task 2 – GNSS in Urban Areas
To enhance the GNSS positioning accuracy utilizing the provided "Urban" dataset, the decoded satellite positions are superimposed onto the sky mask for visibility analysis. Satellite-specific weights are subsequently adjusted in accordance with the sky mask to optimize positioning precision. The experimental results can be reproduced by executing the tracking_POS_updated.m script. During initialization parameters configuration, the solution mode is selected through modification of the solu.mode parameter: 0 corresponds to Ordinary Least Squares (OLS), 1 denotes Weighted Least Squares (WLS), and 2 indicates the Sequential Time-localized Kalman Filter (STL KF). This case study employs both WLS and Extended Kalman Filter (EKF) methodologies, with positioning outcomes derived from optimal weighting selection presented in the **Fig.1** and **Fig.2**.

**Table 1** compares the 3D positioning performance (in terms of RMSE and STD) across different methods with and without applying a skymask. The results show that both EKF and WLS methods benefit from the skymask, as it reduces positioning error. Specifically, EKF with skymask achieves the best performance, with the lowest RMSE (41.68 m) and STD (3.02 m). Although WLS with skymask also improves over WLS alone, its accuracy is significantly lower than the EKF-based methods.

<div align="center">
  <figure>
    <img src="https://github.com/HANG0413/AAE6102-Assignment1/blob/master/Opensky%20Acquisition%20Result.png" width="800">
    <figcaption>
      <b>Fig. 1</b><br> Positioning comparison with and without skymask(EKF).
    </figcaption>
  </figure>
</div>


<div align="center">
  <figure>
    <img src="https://github.com/HANG0413/AAE6102-Assignment1/blob/master/Urban%20Acquisition%20Result.png" width="800">
    <figcaption>
      <b>Fig. 2</b><br> Positioning comparison with and without skymask(WLS).
    </figcaption>
  </figure>
</div>


<p align="center"><b>📊 Table 1 – Comparison on 3D RMSE and STD</b></p>

<table align="center">
  <thead>
    <tr>
      <th style="text-align:center">Method</th>
      <th style="text-align:center">RMSE</th>
      <th style="text-align:center">STD</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">EKF</td>
      <td align="center">49.2223</td>
      <td align="center">3.6630</td>
    </tr>
    <tr>
      <td align="center">EKF with skymask</td>
      <td align="center">41.6839</td>
      <td align="center">3.0196</td>
    </tr>
    <tr>
      <td align="center">WLS</td>
      <td align="center">89.9897</td>
      <td align="center">60.5674</td>
    </tr>
    <tr>
      <td align="center">WLS with skymask</td>
      <td align="center">88.8351</td>
      <td align="center">51.5133</td>
    </tr>
  </tbody>
</table>

## 🛠️ Task 3 – GPS RAIM (Receiver Autonomous Integrity Monitoring)

**Goal:**  Detect and exclude faulty or low-quality GPS measurements using a classic weighted RAIM algorithm.

**RAIM (Receiver Autonomous Integrity Monitoring)** is a method used in GNSS to:
- Detect faults in satellite measurements (outliers)
- Exclude them from the positioning solution
- Monitor the integrity and reliability of position estimates

The **weighted RAIM** version enhances classical RAIM by:
- Incorporating measurement variances (via weights)
- Making the detection more sensitive to low-quality measurements

---

### ✅ Implementation Steps for Weighted RAIM Algorithm

**1. Base WLS Formulation (Already Done)**  
- Input: Observed pseudoranges **z**  
- Observation matrix **H**  
- Weight matrix **W = Σ⁻¹**  
- Position update:  
  ```
  x̂ = (Hᵀ W H)⁻¹ Hᵀ W z
  ```

**2. Compute Post-fit Residuals**  
After solving for position **x̂**, compute the residuals:  
```
r = z - H x̂
```

**3. Compute Test Statistic (Global Test for Fault Detection)**  
Define the test statistic:  
```
T = rᵀ W r
```  
Compare this to a threshold based on a chi-square distribution:  
```
T > χ²ₙ₋ₘ,α
```

Where:  
- **n**: number of measurements (satellites)  
- **m**: number of unknowns (typically 4: x, y, z, clock bias)  
- **α**: confidence level (e.g., 0.001 or 0.005)  

If **T** exceeds the threshold, a fault is detected.

**4. Fault Isolation: Identify and Remove Faulty Measurement**  
Use **RAIM subset testing**:  
1. For each satellite *i*, exclude it temporarily and recompute the WLS solution  
2. Compute the residual norm for each subset  
3. Identify the exclusion that leads to the lowest residual norm — likely the faulty satellite  
4. Remove that satellite and rerun WLS  

**5. Iterate if Necessary**  
Optionally, repeat the process if multiple faults are suspected:  
- Recalculate residuals and test statistic after each exclusion  
- Repeat fault detection and removal until no faults are detected

<div align="center">
  <figure>
    <img src="https://github.com/HANG0413/AAE6102-Assignment1/blob/master/Opensky%20Acquisition%20Result.png" width="800">
    <figcaption>
      <b>Fig. 1</b><br> Positioning comparison with and without skymask(EKF).
    </figcaption>
  </figure>
</div>

## 🛰️ Task 4 – LEO Satellites for Navigation

**Model:** ChatGPT 4o  
**Prompt:**  
Low Earth Orbit (LEO) satellites are widely used for communication purposes but present unique challenges when utilized for navigation.  
Write a short essay (500–1000 words) discussing:  
**The difficulties and challenges of using LEO communication satellites for GNSS navigation.**

---

Low Earth Orbit (LEO) satellites, typically orbiting at altitudes between 500 and 2000 kilometers, have revolutionized global communications, offering low-latency internet and real-time connectivity through constellations like Starlink and OneWeb. Given their growing presence and advanced technology, researchers have explored leveraging LEO satellites for Global Navigation Satellite System (GNSS) purposes, either to augment or even partially replace traditional Medium Earth Orbit (MEO) GNSS systems like GPS, Galileo, and BeiDou. However, adapting LEO communication satellites for navigation introduces a series of technical and operational challenges. This essay discusses the primary difficulties associated with using LEO satellites for GNSS navigation.

---

### 1. High Satellite Dynamics

One of the most fundamental challenges is the high relative motion of LEO satellites. Unlike traditional GNSS satellites that appear relatively stationary over short periods, LEO satellites move rapidly across the sky, completing an orbit in approximately 90–120 minutes. As a result:

- Satellites are visible to a ground user for only a few minutes  
- Frequent satellite handovers are required  
- Rapidly changing Doppler shifts occur, complicating signal tracking  

Navigation receivers must operate with high update rates, rapid reacquisition abilities, and sophisticated Doppler compensation algorithms, significantly increasing receiver complexity compared to traditional GNSS devices.

---

### 2. Limited Visibility and Coverage

Because LEO satellites have a smaller footprint on the Earth's surface (compared to MEO GNSS satellites that cover vast areas), users can typically "see" fewer LEO satellites at any given time. For reliable 3D positioning, a receiver needs signals from at least four satellites simultaneously. Therefore:

- Massive constellations (hundreds to thousands of satellites) are required to ensure continuous global coverage  
- The geometric dilution of precision (GDOP) may fluctuate significantly, leading to variable positioning accuracy  

Maintaining robust coverage demands careful constellation design and may still leave coverage gaps in extreme polar or urban canyon environments.

---

### 3. Signal Design and Strength Challenges

LEO communication satellites are primarily optimized for data transfer rather than precise positioning. Their signals:

- Are often wideband and highly directional (beam-focused) toward ground terminals, not optimized for broad-based navigation use  
- May experience frequent signal blockage in urban environments due to low elevation angles  
- Are subject to higher path loss due to their lower altitudes, requiring careful power management  

Moreover, because the signal characteristics differ from traditional GNSS (which uses structured, spread-spectrum signals like C/A code or P(Y) code), adapting receivers to extract timing and pseudorange information from communication-oriented signals adds significant technical difficulty.

---

### 4. Time Synchronization and Orbit Prediction

Traditional GNSS satellites are tightly synchronized to atomic clocks and operate on highly stable, well-known orbits, allowing precise pseudorange computation. In contrast, LEO communication satellites:

- May not have onboard atomic clocks  
- May not maintain tight synchronization suitable for navigation without modification  
- May follow dynamically adjusted orbits (due to atmospheric drag, station-keeping maneuvers), complicating orbit prediction  

Without highly accurate ephemeris and clock correction data, user devices cannot compute precise positions. Delivering real-time, high-accuracy ephemeris and clock data to millions of users is itself a daunting technical challenge.

---

### 5. Infrastructure and Standardization Issues

To repurpose LEO constellations for navigation:

- New signal standards, modulation techniques, and message structures need to be defined  
- Coordination with existing GNSS systems must be carefully managed to prevent harmful interference  
- Terrestrial infrastructure (e.g., ground control stations, augmentation systems) may need upgrades to support precise orbit and clock determination  

This requires not only massive investment but also international cooperation and regulatory adjustments, potentially slowing large-scale adoption.

---

### 6. Power Consumption and Cost Considerations

Smartphone-grade GNSS receivers are designed to be lightweight and power-efficient, continuously tracking signals from relatively stable satellites. By contrast:

- Tracking fast-moving LEO satellites demands faster signal processing and more frequent handovers, leading to higher receiver power consumption  
- Specialized antennas or multi-frequency tracking capabilities may be needed to maintain performance, increasing device complexity and cost  

This creates trade-offs between positioning performance, battery life, and device affordability, particularly critical for mass-market applications.

---

### ✅ Conclusion

While LEO satellites hold exciting promise for enhancing navigation—offering faster signal acquisition, stronger signals, and potential centimeter-level accuracy when combined with advanced techniques like PPP-RTK—adapting communication satellites for reliable GNSS usage is far from straightforward.

Key challenges include high satellite dynamics, limited instantaneous visibility, non-optimized signal structures, synchronization issues, and significant infrastructure demands. Overcoming these hurdles will require innovations in signal design, receiver architecture, orbital management, and international cooperation.

Nevertheless, with the rapid expansion of LEO constellations and growing research investment, hybrid navigation systems combining traditional GNSS with LEO-based services may well become a defining feature of the next generation of positioning technology.

## 🌍 Task 5 – GNSS Remote Sensing

**Model:** ChatGPT 4o  
**Prompt:**  
GNSS is not only used for positioning and navigation but also has significant applications in remote sensing.  
Write a short essay (500–1000 words) discussing the impact of GNSS in remote sensing.  
Please select one of the following topics covered in the lecture to discuss:
- GNSS Reflectometry (GNSS-R)  
- GNSS Interferometric Reflectometry (GNSS-IR)  
- GNSS Radio Occultation (GNSS-RO)  
- Ionosphere mapping based GNSS ground station  
- GNSS seismology  

---

## The Impact of GNSS in Remote Sensing: GNSS Radio Occultation (GNSS-RO)

Global Navigation Satellite Systems (GNSS) are traditionally associated with positioning, navigation, and timing services. However, in recent decades, GNSS has also become a vital tool in the field of remote sensing, providing new methods to observe the Earth's atmosphere, surface, and oceans. Among these applications, **GNSS Radio Occultation (GNSS-RO)** has emerged as a powerful technique to remotely sense atmospheric properties with remarkable precision and global coverage. This section explores the principles of GNSS-RO, its advantages, and its practical impact.

---

### 🌐 Principles of GNSS Radio Occultation

GNSS-RO relies on the concept of **radio occultation**, where a GNSS satellite sets or rises behind the Earth’s horizon as seen from a Low Earth Orbit (LEO) satellite. As the GNSS signal passes through the atmosphere, it experiences bending, delay, and attenuation due to temperature, pressure, humidity, and ionospheric electron density.

A LEO satellite equipped with a GNSS receiver records changes in the signal’s phase and amplitude. Scientists analyze these measurements to derive **atmospheric refractivity**, and further retrieve temperature, pressure, humidity, and ionospheric profiles.

---

### ✅ Advantages of GNSS-RO

**1. High Accuracy and Vertical Resolution**  
- Excellent precision, especially in the lower and middle atmosphere  
- Not reliant on external calibration sources

**2. All-Weather, Day-and-Night Operation**  
- Operates through clouds, rain, and darkness  
- Superior to visible/infrared techniques in consistency

**3. Truly Global Coverage**  
- LEO-GNSS constellations enable coverage of oceans, polar regions, and data-sparse areas

**4. Climate Monitoring Stability**  
- Highly stable and consistent long-term records  
- Ideal for detecting subtle climate trends

---

### 📊 Applications and Impact

**1. Numerical Weather Prediction (NWP)**  
- GNSS-RO data is assimilated into global/regional forecast models  
- Improves accuracy in upper troposphere and lower stratosphere  
- Used by ECMWF, NOAA, JMA, and others

**2. Climate Research**  
- Long-term temperature trend detection  
- Avoids radiometer drift and sensor bias issues  
- Crucial for studies on global warming and atmospheric change

**3. Space Weather & Ionospheric Monitoring**  
- Provides electron density profiles  
- Helps assess space weather impact on satellites and communications

**4. Tropopause and Composition Studies**  
- Detailed measurements across the tropopause boundary  
- Supports research on ozone transport, water vapor, and trace gases

---

### ⚠️ Challenges and Future Directions

- **Limited Events**: The number of occultation events is limited by GNSS-LEO pairings  
- **Lower-Troposphere Accuracy**: Multipath and diffraction degrade near-surface data  

**Future improvements include:**
- Launching more RO-capable satellites (e.g., COSMIC-2)  
- Using modern GNSS signals (GPS L2C, Galileo, BeiDou)  
- Enhancing retrieval algorithms for complex atmospheric conditions

---

### 🧩 Conclusion

GNSS Radio Occultation (GNSS-RO) is one of the most transformative remote sensing techniques derived from navigation systems. It delivers:

- High-precision, long-term stable atmospheric data  
- Critical inputs for weather forecasting, climate monitoring, and space environment studies  
- Robust performance under all weather and lighting conditions  

As GNSS and LEO satellite networks continue expanding, GNSS-RO will become even more integral to Earth observation, meteorology, and environmental science.

[1] B. Xu and L.-T. Hsu, ‘Open-source MATLAB code for GPS vector tracking on a software-defined receiver’, *GPS Solut*, vol. 23, no. 2, p. 46, Apr. 2019, doi: [10.1007/s10291-019-0839-x](https://doi.org/10.1007/s10291-019-0839-x).

[2] H.-F. Ng, G. Zhang, K.-Y. Yang, S.-X. Yang, and L.-T. Hsu, ‘Improved weighting scheme using consumer-level GNSS L5/E5a/B2a pseudorange measurements in the urban area’, *Advances in Space Research*, vol. 66, no. 7, pp. 1647–1658, Oct. 2020, doi: [10.1016/j.asr.2020.06.002](https://doi.org/10.1016/j.asr.2020.06.002).

[3] OpenAI. (2025, April 30). ChatGPT model response on GNSS Techniques. Retrieved from https://www.openai.com/chatgpt.

[4] Walter, T., & Enge, P. (1995, September). Weighted RAIM for precision approach. In Proceedings of Ion GPS (Vol. 8, No. 1, pp. 1995-2004). Institute of Navigation. https://web.stanford.edu/group/scpnt/gpslab/pubs/papers/Walter_IONGPS_1995_wraim.pdf

