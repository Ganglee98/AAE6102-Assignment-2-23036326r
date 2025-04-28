# Assignment-2


## Assignment Tasks

### Task 1 – Differential GNSS Positioning
Write a short essay (500–1000 words) comparing the pros and cons of the following GNSS techniques for smartphone navigation:

- **Differential GNSS (DGNSS)**
- **Real-Time Kinematic (RTK)**
- **Precise Point Positioning (PPP)**
- **PPP-RTK**



#### GNSS Techniques for Smartphone Navigation （poe o1 link:  https://poe.com/s/6jfp5Iqu9jVZzk2maFkI）

The evolution of Global Navigation Satellite System (GNSS) technology has introduced various techniques to enhance positional accuracy, particularly for smartphone navigation. Among these techniques, Differential GNSS (DGNSS), Real-Time Kinematic (RTK), Precise Point Positioning (PPP), and the hybrid PPP-RTK each offer distinct advantages and challenges.

DGNSS improves location accuracy by comparing data from a receiver of unknown location, like a smartphone, to a reference receiver at a known location. The reference station calculates corrections based on the discrepancies between the satellite signals it receives and its known position. These corrections are transmitted in real time, significantly reducing errors caused by satellite clock drift or atmospheric delays. One of the main advantages of DGNSS is its relative simplicity, as it requires modest computational power and is easier to implement on smartphones compared to more complex techniques. Additionally, DGNSS can achieve accuracy levels of approximately 1–3 meters and is supported by numerous public networks, making it widely accessible. However, its limitations include the difficulty of achieving sub-meter precision, dependence on the proximity of reference stations, and the requirement for a real-time data link, which can increase communication costs and battery usage.

RTK positioning takes accuracy a step further by utilizing phase measurements of GNSS signals instead of just code measurements, allowing for centimeter-level precision in real time. Like DGNSS, RTK relies on reference stations, but it leverages carrier phase measurements to dramatically reduce positional errors. RTK is celebrated for its high accuracy and rapid convergence, often achieving full precision within seconds in optimal conditions. This technique has become an industry standard for applications demanding high precision, such as geodesy and precision agriculture. However, RTK's complexity and costs can be prohibitive, as it requires high-quality GNSS receivers and antennas that may not fit within smartphone hardware constraints. Furthermore, dense urban environments can interfere with signal tracking, leading to reduced accuracy, and RTK's reliance on nearby reference stations creates additional challenges related to data usage and power consumption.

In contrast, PPP eliminates the need for local reference stations by applying global orbital and clock corrections for each satellite, allowing a single GNSS receiver to estimate its position with high accuracy, typically within a few centimeters or decimeters under ideal conditions. The primary advantage of PPP lies in its independence from local infrastructure, making it suitable for areas lacking dense reference station networks. Corrections can be delivered via satellite broadcasts or the internet, offering flexibility in remote regions. However, PPP is hindered by a long initial convergence time, which can take several minutes to half an hour, depending on environmental conditions. Moreover, the technique requires high-quality receivers capable of making accurate carrier-phase measurements, which can be challenging for smartphone hardware. While offline PPP can achieve impressive accuracy, real-time positioning often necessitates subscription-based correction services, adding to the overall cost.

The PPP-RTK hybrid model seeks to combine the strengths of both PPP and RTK, offering global corrections while rapidly resolving carrier-phase ambiguities. This approach aims to deliver near-RTK-level accuracy without the need for proximity to local reference stations. One of the standout features of PPP-RTK is its fast convergence, which can be achieved by incorporating atmospheric corrections from regional networks. In optimal conditions, PPP-RTK can provide centimeter-level accuracy comparable to traditional RTK solutions. However, it still faces challenges, including the reliance on specialized correction services that may incur subscription costs and a requirement for advanced hardware to handle real-time ambiguity resolution.

In conclusion, each GNSS enhancement technique presents a unique balance of accuracy, convergence time, and infrastructure requirements. For routine smartphone navigation, where meter-level accuracy is typically sufficient, DGNSS provides a practical and accessible solution. In contrast, applications requiring consistent sub-meter or centimeter accuracy may benefit from RTK, PPP, or PPP-RTK. RTK remains ideal in environments with dense base station networks, while PPP excels in remote areas lacking local infrastructure, albeit with longer convergence times. Ultimately, as GNSS technology continues to advance, these high-precision techniques are likely to become standard features in next-generation smartphone navigation, enhancing user experience and expanding the possibilities for location-based services.





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

### Task 5 – GNSS Remote Sensing
Write a short essay (500–1000 words) discussing the impact of GNSS in remote sensing. Choose one of the following topics:

- **GNSS Reflectometry (GNSS-R)**
- **GNSS Interferometric Reflectometry (GNSS-IR)**
- **GNSS Radio Occultation (GNSS-RO)**
- **Ionosphere mapping based on GNSS ground station**
- **GNSS seismology**
