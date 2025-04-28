# Assignment-2


## Assignment Tasks

## Task 1 – Differential GNSS Positioning
Write a short essay (500–1000 words) comparing the pros and cons of the following GNSS techniques for smartphone navigation:

- **Differential GNSS (DGNSS)**
- **Real-Time Kinematic (RTK)**
- **Precise Point Positioning (PPP)**
- **PPP-RTK**

## Task 2 – GNSS in Urban Areas
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

## Task 4 – LEO Satellites for Navigation
Write a short essay (500–1000 words) discussing the difficulties and challenges of using LEO communication satellites for GNSS navigation.

## Task 5 – GNSS Remote Sensing
Write a short essay (500–1000 words) discussing the impact of GNSS in remote sensing. Choose one of the following topics:

- **GNSS Reflectometry (GNSS-R)**
- **GNSS Interferometric Reflectometry (GNSS-IR)**
- **GNSS Radio Occultation (GNSS-RO)**
- **Ionosphere mapping based on GNSS ground station**
- **GNSS seismology**
