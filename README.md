# Tschool-bootcamp-device-ref

 - The feature mask is a bit field that provides information about which features are exported by the board. Currently, bits are mapped in the following way:
  
   |Bit|31|30|29|28|27|26|25|24|23|22|21|20|19|18|17|16|
   |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
   |Feature|Analog|ADPCM Sync|Switch|Direction of arrival|ADPCM Audio|Microphone Level|Proximity|Luxmeter|Accelerometer|Gyroscope|Magnetometer|Pressure|Humidity|Temperature|Battery|Second Temperature|
   
   |Bit|15|14|13|12|11|10|9|8|7|6|5|4|3|2|1|0|
   |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
   |Feature|CO Sensor|DC Motor|Stepper Motor|SD Logging|Beam forming|Accelerometer Event|Free Fall|Sensor Fusion Compact|Sensor Fusion|Motion Intensity|Compass|Activity|Carry Position|Proximity Gesture|MEMS Gesture|Pedometer|

### Characteristics/Features
The characteristics managed by the SDK must have a UUID as follows: <code>XXXXXXXX-0001-11e1-ac36-0002a5d5c51b</code>.
The SDK scans all the services, searching for characteristics that match the pattern. 

The first part of the UUID has bits set to "1" for each feature exported by the characteristics.

In case of multiple features mapped onto a single characteristic, the data must be in the same order as the bit mask.

A characteristic's data format must be the following:
 
| Length |     2     |         >1         |          >1         |       |
|:------:|:---------:|:------------------:|:-------------------:|:-----:|
|  Name  | Timestamp | First Feature Data | Second Feature Data | ..... |
  
 The first 2 bytes are used to communicate a timestamp. This is especially useful to recognize any loss of data.
 
 Since the BLE packet maximum length is 20 bytes, the maximumm size of a feature's data field is 18 bytes.
 
