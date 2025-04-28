# Assignment-2


## Assignment Tasks

### Task 1 – Differential GNSS Positioning
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





### Task 2 – GNSS in Urban Areas
Urban areas present significant challenges to GNSS positioning due to signal blockage, multipath effects, and poor satellite visibility. 

**Objective:**
Improve the GNSS positioning performance using the "Urban" data provided. The ground truth in geodetic coordinates is:
- Latitude: 22.3198722
- Longitude: 114.209101777778
- Altitude: 3.0 m

**Hint:** Use the skymask to identify satellite visibility blockage.

## Task 3 – GPS RAIM (Receiver Autonomous Integrity Monitoring)
Develop a classic weighted RAIM algorithm to improve and monitor positioning performance.

**Requirements:**
- Implement a weighted RAIM algorithm using the provided “Open-Sky” data.
- Effectively detect and exclude faulty or low-quality measurements.

**Bonus:**
- Compute the 3D protection level (PL) with a probability of false alarm (P_fa) of \(10^{-2}\) and missed detection (P_md) of \(10^{-7}\). Use a GPS pseudorange measurement sigma (σ) of 3m.
- Evaluate GNSS integrity monitoring performance using a Stanford Chart analysis with a 3D alarm limit (AL) of 50 meters.

### Task 4 – LEO Satellites for Navigation
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




### Task 5 – GNSS Remote Sensing
Write a short essay (500–1000 words) discussing the impact of GNSS in remote sensing. Choose one of the following topics:

- **GNSS Reflectometry (GNSS-R)**
- **GNSS Interferometric Reflectometry (GNSS-IR)**
- **GNSS Radio Occultation (GNSS-RO)**
- **Ionosphere mapping based on GNSS ground station**
- **GNSS seismology**
