# README.md

# Mandarin Throat-Vibration-to-Voice-Conversion Open Source Speech Data

This manual introduces the experimental methods and details of open source speech data.

## Experimental Method

To insure the quality of AC speech, we record both voice and vibration signal within an anechoic chamber . Record voice at about 5 centimeters away from condenser microphone (RØDE VideoMic NTG) and vibration signal with four testing accelerometer devices both via a DAQ system (NI-9234 & cDAQ-9171). And preprocess the raw data in four steps:

1. Resample: 25.6 kHz to 16 kHz
2. HPF @ 10 Hz
3. Normalize / None ( “_processed” / none )
4. TLCC Aligning / None ( “_processed” / none )

## Open Source Speech Data

### DUT

The following are the device under test:

1. 352c22 (piezoelectric accelerometers, PCB Piezotronics)
2. 352c33 (piezoelectric accelerometers, PCB Piezotronics)
3. FPC_ADXL335 （Commercial MEMS accelerometer in FPC）
4. FPC_ADXL354 （Commercial MEMS accelerometer in FPC）

### Speech Data

Folder /Recordings contains four kinds of speech data with different devices. Each folder contain two vibration signal and two voice signal:

1. /acc  
    - Vibration signal after the first and second steps of preprocessing.
    - In order to avoid clipping in .wav (+1，-1), we multiple a coefficient  value ‘avoid_clipping_coefficient’
    - Units: g/avoid_clipping_coefficient
2. /acc_processed
    - Vibration signal after all steps of preprocessing.
    - The normalized signal does not include an 'avoid_clipping_coefficient'.
    - These may be zero padding at the begin or the end of sequential signal which is caused by the aligning.
3. /mic
    - Voice signal after the first and second steps of preprocessing.
    - Units: V
4. /mic_processed
    - Voice signal after all steps of preprocessing.
    - These are 100 frames zero padding at both the begin and the end of sequential signal which is caused by the aligning.
5. details.txt
    - Contains essential parameters
        1. Lag
        2. Clipping avoid
        3. Mic parameters

### SAL and SPL reconstruction

1. SAL (Skin Acceleration Level)
    - /acc signal divided by 'avoid_clipping_coefficient' ( g/avoid_clipping_coefficient to g )
    - ACC ÷ 'avoid_clipping_coefficient'
    - And turns into dB @ ref = 0.01 g
2. SPL (Sound Pressure Level)
    - /mic signal divided by (Mic sensitivity multiple Electrical gain)   ( V to Pa )
    - MIC ÷ (sensitivity × Electrical gain)
    - And turns into dB @ ref = 20 μPa