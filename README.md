# IITISoC-24-IVR5-State-Estimation-with-Limited-Sensors

## Goal:
To Implement a robust State Estimation algorithm that keeps computational efficiency in mind and could be deployed on NVIDIA Jetson Xavier Board or even a Raspberry Pi board.

People Involved : 

Mentors:
- [Arjun S Nair](https://github.com/arjun-593)
- [Soham Pandit](https://github.com/Scav6411)
- [Ampady B R](hgitttps://github.com/ampady06)

Members:
<br>
- [Inturi Siva Rishitha](https://github.com/SivaRishitha)
- [Varikuti Reethika Prasanna](https://github.com/Reethika1115)



# State-Estimation-with-Limited-Sensors

## Estimating State of an Autonomous Vehicle

In this project, we have estimated the state of our autonomous vehicle by fusing the data from the sensors IMU, GNSS reciever, and a LiDAR. These sensors provide measurements of varying reliability and at different rates. We have fused the data from these sensors using EXTENDED KALMAN FILTER(EKF). 

The KALMAN FILTER includes a motion model that tells us how the state evolves over time. It updates a state estimate through two stages:



- Prediction using the motion model.
- Correction using the measurement model.



EKF uses linearization to adapt the Kalman Filter to non linear systems.

 Linearization works by computing a local linear approximation to a non linear function about a chosen operating point. It relies on computing Jacobian matrices, which contain all the first order partial derivatives of a function.
 ![image alt](https://github.com/SivaRishitha/IITISoC-24-IVR5-State-Estimation-with-Limited-Sensors/blob/96a6fe895f0cd75679560f4cfb5a50b5650e198a/ekf%202.jpg) ![image alt](https://github.com/SivaRishitha/IITISoC-24-IVR5-State-Estimation-with-Limited-Sensors/blob/bc2d59ddabce6dab9268a22aacb298e7393e41b1/ekf%201.jpg)

 
## Test 1: normal case

First of all, testing the performance of the estimation with normal sensor measurements. The model is able to provide accurate estimate within error range.
![image alt](https://github.com/SivaRishitha/IITISoC-24-IVR5-State-Estimation-with-Limited-Sensors/blob/5cd97d9380ad0befe0803b328ed75abe632291ec/ESTIMATED(pt_1).png)
![image alt](https://github.com/SivaRishitha/IITISoC-24-IVR5-State-Estimation-with-Limited-Sensors/blob/a0678e1742dece702b312d5af7b124ea12677d66/ERROR_PLOTS.png)


## Test 2: wrong extrinsic calibration

In orfer to test out the reliability of the state estimation, an intentional error is applied on the rotational matrix when transforming the reference frame of the LIDAR, resulting unreliable LIDAR measurements. By increasing the variance of the LIDAR estimated error, the model adapts and still performs well.
![image alt](https://github.com/SivaRishitha/IITISoC-24-IVR5-State-Estimation-with-Limited-Sensors/blob/f737b97cf7042755035bfbfa04a862a7e2057ceb/miscalibration%20estimated%20state.png)
![image alt](https://github.com/SivaRishitha/IITISoC-24-IVR5-State-Estimation-with-Limited-Sensors/blob/42013fad784d4b4bff32f23ed382eef6f9f3932f/miscalibration%20errorplots.png)


## Test 3: sensor measurement dropout

A portion of the GNSS and LIDAR data is intentionally erased to test the performance of the estimation when only IMU is available. (like vehicle entering a tunnel)
Although there exists a small shift in height estimation due to the wrong estimation of pitch angle, the model quickly adjusted state estimation of pitch angle and can perform as expected within a reasonable time and error range.
![image alt](https://github.com/SivaRishitha/IITISoC-24-IVR5-State-Estimation-with-Limited-Sensors/blob/3419387b3d50436ab31be8fc5665d7a4ef44d23d/ESTIMATED%20STATE(PT3).png)
![image alt](https://github.com/SivaRishitha/IITISoC-24-IVR5-State-Estimation-with-Limited-Sensors/blob/0362b989e517cb38079c3a2bbd6096c266ad45c4/ERROR_PLOTS(PT3).png)


## Reference:

https://github.com/Vinohith/Self_Driving_Car_specializations
