# Assignment-2


## Assignment Tasks

## Task 1 – Differential GNSS Positioning
Write a short essay (500–1000 words) comparing the pros and cons of the following GNSS techniques for smartphone navigation:

- **Differential GNSS (DGNSS)**
- **Real-Time Kinematic (RTK)**
- **Precise Point Positioning (PPP)**
- **PPP-RTK**



Comparsion of GNSS Techniques for Smartphone Navigation （poe o1 link:  https://poe.com/s/6jfp5Iqu9jVZzk2maFkI）

The evolution of Global Navigation Satellite System (GNSS) technology has introduced various techniques to enhance positional accuracy, particularly for smartphone navigation. Among these techniques, **Differential GNSS (DGNSS)**, **Real-Time Kinematic (RTK)**, **Precise Point Positioning (PPP)**, and the hybrid **PPP-RTK** each offer distinct advantages and challenges.

**DGNSS** improves location accuracy by comparing data from a receiver of unknown location, such as a smartphone, to a reference receiver at a known location. The reference station calculates corrections based on the discrepancies between the satellite signals it receives and its known position. These corrections are transmitted in real time, significantly reducing errors caused by satellite clock drift or atmospheric delays. One of the main advantages of **DGNSS** is its relative simplicity, as it requires modest computational power and is easier to implement on smartphones compared to more complex techniques. Additionally, **DGNSS** can achieve accuracy levels of approximately 1–3 meters and is supported by numerous public networks, making it widely accessible. However, its limitations include the difficulty of achieving sub-meter precision, dependence on the proximity of reference stations, and the requirement for a real-time data link, which can increase communication costs and battery usage.

**RTK** positioning takes accuracy a step further by utilizing phase measurements of GNSS signals instead of just code measurements, allowing for centimeter-level precision in real time. Like **DGNSS**, **RTK** relies on reference stations but leverages carrier phase measurements to dramatically reduce positional errors. **RTK** is celebrated for its high accuracy and rapid convergence, often achieving full precision within seconds under optimal conditions. This technique has become an industry standard for applications demanding high precision, such as geodesy and precision agriculture. However, **RTK**'s complexity and costs can be prohibitive, as it requires high-quality GNSS receivers and antennas that may not fit within smartphone hardware constraints. Furthermore, dense urban environments can interfere with signal tracking, leading to reduced accuracy, and **RTK**'s reliance on nearby reference stations creates additional challenges related to data usage and power consumption.

In contrast, **PPP** eliminates the need for local reference stations by applying global orbital and clock corrections for each satellite, allowing a single GNSS receiver to estimate its position with high accuracy, typically within a few centimeters or decimeters under ideal conditions. The primary advantage of **PPP** lies in its independence from local infrastructure, making it suitable for areas lacking dense reference station networks. Corrections can be delivered via satellite broadcasts or the internet, offering flexibility in remote regions. However, **PPP** is hindered by a long initial convergence time, which can take several minutes to half an hour, depending on environmental conditions. Moreover, the technique requires high-quality receivers capable of making accurate carrier-phase measurements, which can be challenging for smartphone hardware. While offline **PPP** can achieve impressive accuracy, real-time positioning often necessitates subscription-based correction services, adding to the overall cost.

The **PPP-RTK** hybrid model seeks to combine the strengths of both **PPP** and **RTK**, offering global corrections while rapidly resolving carrier-phase ambiguities. This approach aims to deliver near-RTK-level accuracy without the need for proximity to local reference stations. One of the standout features of **PPP-RTK** is its fast convergence, which can be achieved by incorporating atmospheric corrections from regional networks. In optimal conditions, **PPP-RTK** can provide centimeter-level accuracy comparable to traditional **RTK** solutions. However, it still faces challenges, including reliance on specialized correction services that may incur subscription costs and a requirement for advanced hardware to handle real-time ambiguity resolution.

In conclusion, each GNSS enhancement technique presents a unique balance of accuracy, convergence time, and infrastructure requirements. For routine smartphone navigation, where meter-level accuracy is typically sufficient, **DGNSS** provides a practical and accessible solution. In contrast, applications requiring consistent sub-meter or centimeter accuracy may benefit from **RTK**, **PPP**, or **PPP-RTK**. Ultimately, as GNSS technology continues to advance, these high-precision techniques are likely to become standard features in next-generation smartphone navigation, enhancing user experience and expanding the possibilities for location-based services.




## Task 2 – GNSS in Urban Areas
Urban areas present significant challenges to GNSS positioning due to signal blockage, multipath effects, and poor satellite visibility.

### Objective
Improve the GNSS positioning performance using the "Urban" data provided. The ground truth in geodetic coordinates is:

Hint: Use the skymask to identify satellite visibility blockage.

### Satellite Positioning with Sky Mask Optimization
% Prepare sky mask data (skymask.mat):

% The data format is a 361×2 matrix:

% Column 1: Azimuth angles (0° to 360°)

% Column 2: Minimum visible elevation angle for each azimuth

![image](https://github.com/user-attachments/assets/2dbb969b-846a-41e9-a1d4-f1345e8ab071)



We compared three weighting schemes using skymask to improve positioning accuracy. 
The first scheme is the weight scheme based on elevation angle, serving as the baseline. 

The second scheme halves the weight of NLOS satellites, resulting in a 2.13% improvement in accuracy compared to the first. 

The third scheme involves dynamic adjustment based on the difference between the address cutoff altitude angle and the satellite altitude angle, achieving an 8% improvement. Despite these enhancements, the overall effectiveness is limited, possibly due to the small number of satellites and the fact that reducing NLOS satellite weights may compromise the contribution of the satellites to the spatial geometric distribution.

**The following figure shows the third dynamic adjustment scheme. According to the skymask, the weight adjustment range of each NLOS satellite is different.**

![image](https://github.com/user-attachments/assets/d3019d36-b856-4045-b05f-565a91512ef9)











|   |   |   |
|---|---|---|
| ① | ② | ③ |
| 71.04 m | 69.52 m | 69.48 m |




## Task 3 – GPS RAIM (Receiver Autonomous Integrity Monitoring)
Develop a classic weighted RAIM algorithm to improve and monitor positioning performance.

**Requirements:**
- Implement a weighted RAIM algorithm using the provided “Open-Sky” data.
- Effectively detect and exclude faulty or low-quality measurements.

**Bonus:**
- Compute the 3D protection level (PL) with a probability of false alarm (P_fa) of \(10^{-2}\) and missed detection (P_md) of \(10^{-7}\). Use a GPS pseudorange measurement sigma (σ) of 3m.
- Evaluate GNSS integrity monitoring performance using a Stanford Chart analysis with a 3D alarm limit (AL) of 50 meters.






## Task 4 – LEO Satellites for Navigation
Write a short essay (500–1000 words) discussing the difficulties and challenges of using LEO communication satellites for GNSS navigation.

The Challenges of Using Low Earth Orbit Satellites for Navigation （poe o1 link:  https://poe.com/s/6jfp5Iqu9jVZzk2maFkI）

Low Earth Orbit (LEO) satellites are most commonly associated with communication services—such as broadband internet, IoT connectivity, and data relay—owing to their generally lower latency and proximity to the Earth’s surface. However, in recent years, there has been growing interest in extending the utility of these satellites to include satellite navigation. **On the surface, it sounds logical: if these spacecraft exist in large constellations and already offer valuable services, why not harness them for positioning, navigation, and timing (PNT) solutions?** Yet, in practice, the use of LEO communication satellites for precise navigation is fraught with considerable difficulties and challenges.

One of the most defining characteristics of LEO satellites is their low orbital altitude, typically ranging from about 160 km to 2,000 km. **While the closeness to Earth can yield stronger signal power at the receiver compared to satellites in Medium Earth Orbit (MEO), it also puts LEO satellites in much faster orbital motion.** A single LEO satellite may circle the Earth in as little as 90 minutes, which means a ground-based user’s receiver must constantly switch between satellites that appear and disappear on the horizon very quickly. **The frequent handovers complicate signal acquisition, tracking, and re-acquisition processes, demanding more robust receiver algorithms.**

The rapid motion of LEO satellites leads to high Doppler shifts, which occur when the frequency of the transmitted signal is modulated by the relative motion between the satellite and the receiver. **For LEO constellations, Doppler frequencies can be substantially larger than those experienced with MEO satellites.** This presents two specific problems: first, receivers need more advanced frequency tracking loops that must be robust to large and rapidly changing Doppler variations. Second, isolating the satellite’s signal from noise becomes more complex, increasing the risk of losing lock on the signal.

To achieve global coverage necessary for a fully operational GNSS, a sufficiently large constellation is required, suitably spaced among orbital planes. **Although modern LEO communication constellations are quite large and growing, they may not be specifically designed for continuous PNT services.** Coverage gaps can occur, particularly at high latitudes. Furthermore, the geometry of satellite positions is crucial for precise navigation solutions. **Traditional GNSS constellations are arranged so that users can see multiple satellites at different angles, minimizing errors.** In contrast, commercial LEO constellations may not provide optimal geometry for positioning.

Effective navigation relies on extraordinarily precise timing. **Minuscule deviations in the satellite’s clock can lead to significant distance errors on the ground.** Traditional GNSS satellites possess atomic clocks and maintain meticulous synchronization. In LEO, satellites typically do not house the same caliber of atomic frequency standards, making synchronization more difficult. **Any hiccup in maintaining accurate time references could severely degrade navigational precision.**

Navigation signals are designed with spreading codes and modulation schemes for robust acquisition and error detection. **LEO communication satellites use signals optimized for data throughput, which may be less suited to precise ranging.** Adapting these signals for navigation would require additional pilot signals or navigation message components, complicating regulatory compliance since the spectrum is often crowded.

While LEO’s proximity to Earth yields stronger signal power, the link budget still needs careful oversight. **Incorporating navigation services could require broadcasting additional signals, modifying the satellite’s overall power budget.** This would necessitate advanced mission architectures and potentially new hardware.

Finally, the idea of “piggybacking” navigation services on large commercial LEO constellations sounds economically appealing, but the reality is more complex. **Providing high-accuracy navigation demands significant system-level changes, including ground control network expansion and precise orbit determination capabilities.** The total cost for implementing these features may turn out to be large, complicating the return on investment for commercial constellation operators.

In conclusion, **while LEO communication satellites hold intriguing potential for navigation services, significant obstacles remain.** The rapid orbital motion demands frequent handovers and sophisticated tracking, while large Doppler shifts complicate signal processing. Constellation geometry, clock synchronization, regulatory concerns, and power allocation each pose additional challenges. **Collaborative efforts between commercial operators and navigation stakeholders may make LEO-based navigation a reality—if these obstacles are systematically addressed.** The global demand for robust navigation solutions presents a strong incentive to adapt LEO satellites for these purposes.




## Task 5 – GNSS Remote Sensing
Write a short essay (500–1000 words) discussing the impact of GNSS in remote sensing. Choose one of the following topics:

- **GNSS Reflectometry (GNSS-R)**
- **GNSS Interferometric Reflectometry (GNSS-IR)**
- **GNSS Radio Occultation (GNSS-RO)**
- **Ionosphere mapping based on GNSS ground station**
- **GNSS seismology**

The Impact of GNSS Radio Occultation on Earth Observation （poe o1 link:  https://poe.com/s/6jfp5Iqu9jVZzk2maFkI）

Satellite-based navigation systems such as GPS, Galileo, GLONASS, and BeiDou, collectively referred to as Global Navigation Satellite Systems (GNSS), originally emerged to meet the world’s positioning, navigation, and timing requirements. However, these signals have proven to be versatile for remote sensing applications, particularly in studying Earth’s atmosphere. One of the most powerful techniques to arise in this domain is **GNSS Radio Occultation (GNSS-RO)**, which leverages the bending of GNSS signals as they pass through the Earth’s atmospheric layers to extract detailed information about temperature, pressure, and humidity profiles. 

**The core principle of GNSS-RO** lies in the refraction of radio waves traveling between a GNSS satellite and a receiver in low Earth orbit (LEO). As a LEO satellite observes a GNSS satellite rising or setting behind the Earth’s limb, the GNSS signals traverse different atmospheric layers at various angles. The resulting changes in signal velocity and path—i.e., the bending—are sensitive to the refractivity of the atmosphere, which is determined by properties such as density, temperature, and water vapor concentration. By measuring signal phase delays and bending angles, scientists can reconstruct vertical profiles of temperature, pressure, and humidity in the troposphere and lower stratosphere.

**GNSS-RO offers significant advantages for meteorology.** It provides global, all-weather, high-vertical-resolution measurements of the atmospheric state, which is critical for improving weather forecasts. Unlike satellite radiometers that struggle in cloudy conditions, GNSS-RO data can be assimilated directly into numerical weather prediction (NWP) models. This capability leads to notable improvements in short- to medium-range weather forecasts, particularly in detecting subtle changes in atmospheric temperature and moisture structure.

Furthermore, one of the standout features of GNSS-RO is its high vertical resolution, especially in the upper troposphere and lower stratosphere. Traditional satellite-based sounding instruments may achieve broader coverage horizontally but often struggle to capture fine vertical gradients. GNSS-RO complements these instruments by offering specialized vertical “slices” through the atmosphere, making it a powerful tool for refining global circulation models.

The impact of GNSS-RO extends beyond immediate weather forecasting; it also plays a crucial role in **climate monitoring**. By providing unbiased, calibration-free profiles of atmospheric refractivity, temperature, and humidity, GNSS-RO has emerged as an important data source for detecting long-term trends associated with climate change. Its relative insensitivity to instrument drift over time reinforces its credibility for climate benchmarking. Moreover, the consistent signals from GNSS satellites ensure minimal measurement bias, a significant advantage over many other Earth observation instruments.

In addition to meteorological and climate applications, GNSS-RO also contributes valuable insights into **space weather**. By analyzing the ionospheric profiling that results from GNSS signal refraction, researchers can determine electron density profiles. This information is crucial for understanding ionospheric dynamics and improving the accuracy of trans-ionospheric communication. Moreover, monitoring changes in the ionosphere enables scientists to track geomagnetic storms and other disturbances triggered by solar activity, which can disrupt communication and navigation systems.

Despite its advantages, GNSS-RO faces several **technical and operational challenges**. A robust GNSS-RO mission requires multiple LEO satellites equipped with dedicated GNSS receivers to capture a high number of occultations daily. Missions like COSMIC and GRACE have demonstrated the power of GNSS-RO but also highlighted the need for continuous satellite missions to ensure reliable data streams. Additionally, tracking GNSS signals at low elevations can be challenging due to atmospheric attenuation and distortion, necessitating advanced receiver designs and algorithms.

In conclusion, **GNSS Radio Occultation has revolutionized our ability to profile the Earth’s atmosphere**, making GNSS far more than just a positioning tool. By exploiting the bending and time delay of radio waves, scientists can derive precise vertical profiles of temperature, pressure, and humidity, thereby improving weather prediction models and enhancing climate monitoring. While operational challenges remain, the continued evolution of GNSS-RO will drive innovations in meteorology, climate science, and space weather research. As GNSS constellations expand and new LEO satellite missions are launched, the scope and precision of GNSS-RO data will undoubtedly continue to shape Earth observation, delivering significant benefits across a wide range of scientific and practical applications.
