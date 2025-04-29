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

**DGNSS** improves positioning accuracy by differencing data from a receiver of unknown location, such as a smartphone, to a reference receiver at a known location. The reference station calculates corrections based on the discrepancies between the satellite signals it receives and its known position. These corrections are transmitted in real time, significantly reducing errors like atmospheric delays. One of the main advantages of **DGNSS** is its relative simplicity, as it requires modest computational power and is easier to implement on smartphones compared to more complex techniques. Additionally, **DGNSS** can achieve meter-level performance and is supported by numerous public networks, making it widely accessible. However, its limitations include the difficulty of achieving sub-meter precision, dependence on the proximity of reference stations.

**RTK** positioning takes accuracy a step further by utilizing phase measurements of GNSS signals instead of just code measurements, allowing for centimeter-level precision in real time. Like **DGNSS**, **RTK** relies on reference stations but leverages carrier phase measurements to dramatically reduce positional errors. **RTK** is celebrated for its high accuracy and rapid convergence, often achieving full precision within seconds under optimal conditions. This technique has become an industry standard for applications demanding high precision, such as geodesy and precision agriculture. However, **RTK**'s complexity and costs can be prohibitive, as it requires high-quality GNSS receivers and antennas that may not fit within smartphone hardware constraints. Furthermore, dense urban environments can interfere with signal tracking, leading to reduced accuracy, and **RTK**'s reliance on nearby reference stations creates additional challenges related to data usage and power consumption.

In contrast, **PPP** eliminates the need for local reference stations by applying global orbital and clock corrections for each satellite, allowing a single GNSS receiver to estimate its position with high accuracy, typically within a few centimeters or decimeters under ideal conditions. The primary advantage of **PPP** lies in its independence from local infrastructure, making it suitable for areas lacking dense reference station networks. Corrections can be delivered via satellite broadcasts or the internet, offering flexibility in remote regions. However, **PPP** is hindered by a long initial convergence time, which can take several minutes to half an hour, depending on environmental conditions. Moreover, the technique requires high-quality receivers capable of making accurate carrier-phase measurements, which can be challenging for smartphone hardware. While offline **PPP** can achieve impressive accuracy, real-time positioning often necessitates subscription-based correction services, adding to the overall cost.

The **PPP-RTK** model seeks to combine the strengths of both **PPP** and **RTK**, offering global corrections while rapidly resolving carrier-phase ambiguities. This approach aims to deliver near-RTK-level accuracy without the need for proximity to local reference stations. One of the standout features of **PPP-RTK** is its fast convergence, which can be achieved by incorporating atmospheric corrections from regional networks. In optimal conditions, **PPP-RTK** can provide centimeter-level accuracy comparable to traditional **RTK** solutions. However, it still faces challenges, including reliance on specialized correction services that may incur subscription costs and a requirement for advanced hardware to handle real-time ambiguity resolution.

In conclusion, each GNSS enhancement technique presents a unique balance of accuracy, convergence time, and infrastructure requirements. For routine smartphone navigation, where meter-level accuracy is typically sufficient, **DGNSS** provides a practical and accessible solution. In contrast, applications requiring consistent sub-meter or centimeter accuracy may benefit from **RTK**, **PPP**, or **PPP-RTK**. Ultimately, as GNSS technology continues to advance, these high-precision techniques are likely to become standard features in next-generation smartphone navigation, enhancing user experience and expanding the possibilities for location-based services.




## Task 2 – GNSS in Urban Areas
Urban areas present significant challenges to GNSS positioning due to signal blockage, multipath effects, and poor satellite visibility.

### Objective
Improve the GNSS positioning performance using the "Urban" data provided. The ground truth in geodetic coordinates is:

Hint: Use the skymask to identify satellite visibility blockage.

### Satellite Positioning with Sky Mask Optimization
% Prepare sky mask data (skymask.mat):

![image](https://github.com/user-attachments/assets/6457e02f-ec68-4291-8f63-12cca005ae14)


% The data format is a 361×2 matrix:

% Column 1: Azimuth angles (0° to 360°)

% Column 2: Minimum visible elevation angle for each azimuth




![image](https://github.com/user-attachments/assets/2dbb969b-846a-41e9-a1d4-f1345e8ab071)



We compared three weighting schemes using skymask to improve positioning accuracy. 
①The first scheme is the weight scheme based on elevation angle, serving as the baseline. 

②The second scheme halves the weight of NLOS satellites. 

③The third scheme involves dynamic adjustment based on the difference between the address cutoff altitude angle and the satellite altitude angle. Despite these enhancements, the overall effectiveness is limited, possibly due to the small number of satellites and the fact that reducing NLOS satellite weights may compromise the contribution of the satellites to the spatial geometric distribution.

**The following figure shows the third dynamic adjustment scheme. According to the skymask, the weight adjustment range of each NLOS satellite is different.**


![2](https://github.com/user-attachments/assets/d0f386bd-4195-417e-a726-13482e938c1d)



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

   ### RAIM
   %===============================================

        % snapshot test statistic
          r = omc - A*x;  % Calculate the residuals
          sse = sqrt(r' * C * r);  % Calculate the sum of squared errors
          dof = length(current_sats) - 4;  % Degrees of freedom

        % chi value
         idx = find(chi2_table(:,1) == length(current_sats), 1);
         if isempty(idx)
          chi2_threshold = chi2inv(1-alpha, dof);  % Calculate chi-squared threshold
         else
          chi2_threshold = chi2_table(idx,2);  % Retrieve threshold from chi-squared table
         end

        % fault detection
         if sse > chi2_threshold
         % find fault
         normalized_res = abs(r) ./ sqrt(diag(inv(C)));  % Normalize residuals
         [~, worst_sat_idx] = max(normalized_res);  % Find the satellite with the maximum normalized residual
          worst_sat = current_sats(worst_sat_idx);
    
          fprintf('Fault detected (SSE=%.3f > threshold=%.3f)\n', sse, chi2_threshold);
          fprintf('Excluding satellite %d (normalized residual=%.3f)\n', worst_sat, max(normalized_res));
    
        % Update satellite list
        faulty_sats = [faulty_sats, worst_sat];  % Add the faulty satellite to the list
        current_sats = setdiff(current_sats, worst_sat);  % Remove the faulty satellite from current satellites
        else
        fprintf('RAIM validation passed (SSE=%.3f <= threshold=%.3f)\n', sse, chi2_threshold);
        break;  % Exit the RAIM loop
        end

![1个fault](https://github.com/user-attachments/assets/938fbfa6-2025-4e2f-bc34-0868005ab742)    ![image](https://github.com/user-attachments/assets/73e70b26-ce16-452c-9357-470316aa0599)




**Bonus:**
### Compute the 3D protection level (PL) with a probability of false alarm (P_fa) of \(10^{-2}\) and missed detection (P_md) of \(10^{-7}\). Use a GPS pseudorange measurement sigma (σ) of 3m.
   ####  Protection Level Calculation
   %================================

   
     %  1. Calculate the projection matrix (using the current A matrix and weights)
   
         m = length(current_sats)+1;
         S = (A' * C * A) \ (A' * C);
         P = A*S;
         
      % 2. Calculate the 3D slope of each satellite
         Slope_3D = zeros(m, 1);
        for i = 1:m
        Slope_3D(i) = sqrt(S(1,i)^2 + S(2,i)^2 + S(3,i)^2) / sqrt(P(i,i));
       end
      
       Slope_3D_max = max(Slope_3D);

     % 3. Get the chi-square threshold (use the same threshold table as RAIM detection)
       idx = find(chi2_table(:,1) == m, 1);
       if isempty(idx)
       T = chi2inv(1-alpha, m-4);
      else
       T = chi2_table(idx,2);
       end

     % 4. Calculate the RMS of the position error
      cov_xyz = inv(A' * C * A);
      RMS_3D = sqrt(cov_xyz(1,1) + cov_xyz(2,2) + cov_xyz(3,3));

    % Step 2: Compute k_md (Gaussian inverse)
     P_md=1e-7;
     k_md = norminv(1 - P_md/2);   % ≈ 5.33 for P_md=1e-7

     k_3D = 3.0;  
     PL = Slope_3D_max * T + k_3D * k_md ;

     fprintf('Protection level calculation: PL_3D = %.2f meters (maximum slope=%.2f, RMS=%.2f)\n',...
     PL, Slope_3D_max, RMS_3D);

     fprintf('Calculate protection level: PL = %.2f meters\n', PL);



   %===============================================
### Evaluate GNSS integrity monitoring performance using a Stanford Chart analysis with a 3D alarm limit (AL) of 50 meters.

#### analysis
The first graph shows two lines: one for Protection Level (PL) and one for Position Error (PE). The blue line represents PL, which is stable and indicates a safe threshold for the system. The red line represents PE, which moves up and down, showing how accurate the system is.

When the PE line is below the PL line, the system is working well, indicating that the position is accurate and safe. However, if the PE line goes above the PL line, it suggests potential problems, meaning the system may not be reliable or safe. Monitoring both PL and PE is important. Keeping PE below PL helps maintain safety and trust in the system.



![pl](https://github.com/user-attachments/assets/0a4571bc-ec20-4672-8f4d-11aae9d335b5)

![untitled](https://github.com/user-attachments/assets/1f6a420e-a97e-498a-97ec-df6afb3aea75)







## Task 4 – LEO Satellites for Navigation
Write a short essay (500–1000 words) discussing the difficulties and challenges of using LEO communication satellites for GNSS navigation.

The Challenges of Using Low Earth Orbit Satellites for Navigation （poe o1 link:  https://poe.com/s/6jfp5Iqu9jVZzk2maFkI）

LEO satellites are primarily recognized for their role in communication services, such as providing broadband internet and enabling Internet of Things (IoT) connectivity. Recently, there has been a growing interest in utilizing these satellites for navigation purposes. While the idea seems logical, given their large constellations and existing infrastructure, several significant challenges must be overcome to make this a reality.

One of the defining characteristics of LEO satellites is their low orbital altitude, typically between 160 km and 2,000 km. This proximity to Earth can yield stronger signal power compared to satellites in Medium Earth Orbit (MEO). **However**, it also results in much faster orbital motion; a single LEO satellite can complete an orbit in as little as 90 minutes. This rapid movement necessitates that ground-based receivers frequently switch between satellites, complicating the processes of signal acquisition, tracking, and re-acquisition.

**Moreover**, the swift motion of LEO satellites leads to high Doppler shifts in the transmitted signals. These shifts occur due to the relative motion between the satellite and the receiver, and they are significantly larger than those experienced with MEO satellites. Consequently, receivers must employ more sophisticated frequency tracking mechanisms that can adapt to these rapid changes. This requirement complicates signal processing, increasing the risk of losing lock on the incoming signals.

To provide the global coverage necessary for effective navigation, a sufficiently large constellation of LEO satellites is crucial. Although many modern LEO communication constellations are extensive and expanding, they may not be designed for continuous positioning, navigation, and timing (PNT) services. Coverage gaps can occur, particularly at higher latitudes, and the geometry of satellite positions is vital for accurate navigation solutions. Traditional GNSS constellations are arranged to ensure that users can see multiple satellites at various angles, which helps minimize errors. In contrast, commercial LEO constellations may not achieve the optimal geometry required for precise positioning.

Accurate navigation also relies on precise timing. Small deviations in a satellite's clock can lead to significant errors in distance calculations on the ground. While traditional GNSS satellites utilize atomic clocks to maintain synchronization, LEO satellites often do not have the same level of timing accuracy, making synchronization more challenging. Any failure to maintain accurate time references could severely degrade navigational precision.

In conclusion, while LEO communication satellites offer intriguing potential for navigation services, substantial obstacles remain. The rapid orbital motion complicates signal tracking, and large Doppler shifts pose additional challenges for receivers. Issues related to coverage, timing accuracy, signal design, and power allocation further complicate the integration of navigation capabilities. Collaborative efforts between commercial satellite operators and navigation stakeholders may help address these challenges, making LEO-based navigation a viable option in the future. The increasing global demand for robust navigation solutions provides a strong incentive to adapt LEO satellites for these purposes.




## Task 5 – GNSS Remote Sensing
Write a short essay (500–1000 words) discussing the impact of GNSS in remote sensing. Choose one of the following topics:

- **GNSS Reflectometry (GNSS-R)**
- **GNSS Interferometric Reflectometry (GNSS-IR)**
- **GNSS Radio Occultation (GNSS-RO)**
- **Ionosphere mapping based on GNSS ground station**
- **GNSS seismology**

The Impact of GNSS Radio Occultation on Earth Observation （poe o1 link:  https://poe.com/s/6jfp5Iqu9jVZzk2maFkI）

Satellite-based navigation systems such as GPS, Galileo, GLONASS, and BeiDou, collectively referred to as Global Navigation Satellite Systems (GNSS), originally emerged to meet the world’s positioning, navigation, and timing requirements. However, these signals have proven to be versatile for remote sensing applications, particularly in studying Earth’s atmosphere. One of the most powerful techniques to arise in this domain is **GNSS Radio Occultation (GNSS-RO)**, which leverages the bending of GNSS signals as they pass through the Earth’s atmospheric layers to extract detailed information about temperature, pressure, and humidity profiles. 

The core principle of GNSS-RO lies in the refraction of radio waves traveling between a GNSS satellite and a receiver in low Earth orbit (LEO). As a LEO satellite observes a GNSS satellite rising or setting behind the Earth’s limb, the GNSS signals traverse different atmospheric layers at various angles. The resulting changes in signal velocity and path—i.e., the bending—are sensitive to the refractivity of the atmosphere, which is determined by properties such as density, temperature, and water vapor concentration. By measuring signal phase delays and bending angles, scientists can reconstruct vertical profiles of temperature, pressure, and humidity in the troposphere and lower stratosphere.

GNSS-RO offers significant advantages for meteorology. It provides global, all-weather, high-vertical-resolution measurements of the atmospheric state, which is critical for improving weather forecasts. Unlike satellite radiometers that struggle in cloudy conditions, GNSS-RO data can be assimilated directly into numerical weather prediction (NWP) models. This capability leads to notable improvements in short- to medium-range weather forecasts, particularly in detecting subtle changes in atmospheric temperature and moisture structure.

Furthermore, one of the standout features of GNSS-RO is its high vertical resolution, especially in the upper troposphere and lower stratosphere. Traditional satellite-based sounding instruments may achieve broader coverage horizontally but often struggle to capture fine vertical gradients. GNSS-RO complements these instruments by offering specialized vertical “slices” through the atmosphere, making it a powerful tool for refining global circulation models.

The impact of GNSS-RO extends beyond immediate weather forecasting; it also plays a crucial role in climate monitoring. By providing unbiased, calibration-free profiles of atmospheric refractivity, temperature, and humidity, GNSS-RO has emerged as an important data source for detecting long-term trends associated with climate change. Its relative insensitivity to instrument drift over time reinforces its credibility for climate benchmarking. Moreover, the consistent signals from GNSS satellites ensure minimal measurement bias, a significant advantage over many other Earth observation instruments.

In addition to meteorological and climate applications, GNSS-RO also contributes valuable insights into space weather. By analyzing the ionospheric profiling that results from GNSS signal refraction, researchers can determine electron density profiles. This information is crucial for understanding ionospheric dynamics and improving the accuracy of trans-ionospheric communication. Moreover, monitoring changes in the ionosphere enables scientists to track geomagnetic storms and other disturbances triggered by solar activity, which can disrupt communication and navigation systems.

Despite its advantages, GNSS-RO faces several technical and operational challenges. A robust GNSS-RO mission requires multiple LEO satellites equipped with dedicated GNSS receivers to capture a high number of occultations daily. Additionally, tracking GNSS signals at low elevations can be challenging due to atmospheric attenuation and distortion, necessitating advanced receiver designs and algorithms.

In conclusion, GNSS Radio Occultation has made GNSS far more than just a positioning tool. As GNSS constellations expand and new LEO satellite missions are launched, the scope and precision of GNSS-RO data will undoubtedly continue to shape Earth observation, delivering significant benefits across a wide range of scientific and practical applications.
