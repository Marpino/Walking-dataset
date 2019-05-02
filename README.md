# Walking-Dataset
This dataset is made of 20 IMUs recordings of people walking 5 meters. The IMUs are positioned on both legs in the foot-shank-thigh configuration. The subjects are 20 elderly people and 20 young people.

# Dataset Organization
The dataset is set in this way:

- There are 20 recordings of eldery people in the folder \Dataset\Elderly and other 20 recordings of young people in the folder \Dataset\Young, both the groups were asked to walk for 5 meters straight.

- There is \Dataset\Additional folder to which belong: 
1) a subfolder Marzia with recordings of me walking 5 meters straight, in a rectagle of 5x3 meters and in a circle of 3.6 meters diameter.
2) a subfolder Long Distance with recordings of me walking randomly in a corridor.
3) a subfolder Disability with 2 recordings of a subject affected by legs muscolar atrophy, walking with sticks and leg braces.

In each folder of \Dataset you can find the recordings in .xlsx format
There are 7 sensors and each one corresponds to a part of the body:
_1 right foot
_2 right shank
_3 right thigh
_4 left thigh
_5 left shank
_6 left foot
(_7 back, but it is not syncronized with the other sensors and in some recordings is not available)

The useful information are:

- Acc_read_x linear acceleration along x 
- Acc_read_y linear acceleration along y
- Acc_read_z linear acceleration along z

- Gyro_read_x angular velocity x 
- Gyro_read_y angular velocity y 
- Gyro_read_z angular velocity z 

- Ext1 pressure toe
- Ext2 pressure heel

# Data Manipulation
In order to use the data you have to:

SCALE 
acc=(acc/10000)*gravity
gyro=(gyro/100)*pi/180

FILTER
Taking into account that the sampling frequency is 100 apply a low pass filter to remove the noise with the cut off frequency around 3 Hz

ROTATE
RIGHT LEG=[0 0 1; 0 1 0; -1 0 0];
LEFT LEG=[0 0 -1; 0 -1 0; -1 0 0];

# Additional Data
There is an additional folder \EstimatedData, with each subfolder corresponding to the dataset.
Inside each subfolder there are 3 files .mat and 7 files .csv and additional files .fig that are matlab plots
- angularRate: scaled, filtered and rotated;
- specificForce: scaled, filtered and rotated; (it is the pure accelerometer output, gravity included)
- orientation (roll,pitch and yaw): estimated;
- position (x,y,z): estimated;
- linear velocity magnitude: estimated;
- zupt(zero velocity update): it is 1 when the foot is supposed to have zero velocity and 0 when the foot is moving;
- T=gyro(k)'*gyro(k)/sigmaG^2+acc(k)'*acc(k)/sigmaA^2. Check if the test statistics T are below the detector threshold. If so, chose the hypothesis that the system has zero velocity.

