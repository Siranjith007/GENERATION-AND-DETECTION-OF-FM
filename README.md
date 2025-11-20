# GENERATION-AND-DETECTION-OF-FM
## AIM:
To write a program for Frequency Modulation and Demodulation using SCILAB and to observe and measure the frequency deviation and the modulation index of FM.

## EQUIPMENTS REQUIRED

•	Computer with i3 Processor

•	SCI LAB

## THEORY
  Frequency modulation is a type of modulation in which the frequency of the high frequency (carrier) is varied in accordance with the instantaneous value of the modulating signal.
  
  #### FREQUENCY DEVIATION Δf  and MODULATION INDEX m f :
  
  The frequency deviation Δf represents the maximum shift between the  modulated signal
  frequency, over and under the frequency of the carrier.
  
  We define modulation index m f the ratio between Δf and the modulating frequency
  m= Δf / fm


#### FREQUENCY MODULATION GENERATION:
  The circuits used to generate a frequency modulation must vary the frequency of a high frequency signal (carrier) as function of the amplitude of a low frequency signal (modulating signal). In practice there are two main methods used to generate FM.

## ALGORITHM
  1.	Define Parameters:
     
      •	Fs: Sampling frequency.
      •	T: Duration of the signal.
      •	Fc: Carrier frequency.
      •	Fm: Frequency of the modulating signal.
      •	Beta: Modulation index, which controls the extent of frequency deviation.
  2.	Generate Signals:
     
      •	modulating_signal: Sinusoidal signal used for modulation.
      •	carrier_signal: The high-frequency carrier signal.
      •	modulated_signal: FM modulated signal calculated by varying the carrier frequency according to the modulating signal.
      
  3.	FM Modulation:
     
      •	Modulated_signal is obtained by modulating the carrier signal with the modulating signal.
 
  4.	FM Demodulation:
     
      •	Differentiation: Computes the derivative of the modulated signal to extract frequency variations.
      •	Envelope Detection: Takes the absolute value to retrieve the envelope of the signal.
      •	Low-pass Filtering: Applies a Butterworth low-pass filter to smooth the envelope and recover the original modulating signal.
      
  5.	Visualization:
      
      •	Plots the modulating signal, carrier signal, FM modulated signal, and demodulated signal for analysis.


## PROCEDURE

    •	Refer Algorithms and write code for the experiment.
    •	Open SCILAB in System
    •	Type your code in New Editor
    •	Save the file
    •	Execute the code
    •	If any Error, correct it in code and execute again
    Verify the generated waveform using Tabulation and Model Waveform

## MODEL GRAPH:
<img width="512" height="365" alt="image" src="https://github.com/user-attachments/assets/dfe6bc64-2b6f-4afa-ae79-95391859ab04" />

## PROGRAM
clc; clear;

am = 7.5; fm = 217.9; fs = 21790; t = 0:1/fs:10/fm; ac = 15; fc = 2179; beta = 5;

msg = am * sin(2 * %pi * fm * t); car = ac * cos(2 * %pi * fc * t); sFM = ac * cos(2 * %pi * fc * t + beta * sin(2 * %pi * fm * t));

z = hilbert(sFM); dz = [diff(z) 0]; inst_omega = imag(dz ./ z); f_inst = (fs / (2 * %pi)) * inst_omega; dev = f_inst - fc;

wc = fm / (fs / 2); if wc > 0.49 then wc = 0.49; end n = 200; h = wfir("lp", n + 1, wc, "hm", 0);

N = length(dev); L = length(h); nf = 3 * (L - 1);

if nf > N - 1 then nf = N - 1; end

if nf < 1 then y = filter(h, 1, dev); demod = y(1:N); else xp = [dev(nf+1:-1:2), dev, dev(
:
−
1
:
-nf)]; y1 = filter(h, 1, xp); y2 = filter(h, 1, y1(
:
−
1
:
1
)
)
;
y
2
=
y
2
(
👎1); demod = y2(nf+1:nf+N); end

demod = demod / max(abs(demod)) * am;

subplot(4,1,1); plot(t, msg); title("Message-Signal"); xlabel("Time - (s)"); ylabel("Amplitude");

subplot(4,1,2); plot(t, car); title("Carrier-Signal"); xlabel("Time - (s)"); ylabel("Amplitude");

subplot(4,1,3); plot(t, sFM); title("FM-Modulated-Signal"); xlabel("Time - (s)"); ylabel("Amplitude");

subplot(4,1,4); plot(t, demod); title("Demodulated-Signal (Zero-phase)"); xlabel("Time - (s)"); ylabel("Amplitude");

## TABULATION

![WhatsApp Image 2025-11-20 at 1 10 32 PM](https://github.com/user-attachments/assets/75200bb1-44f2-4600-865a-c7d716e9ae55)

## CALCULATION

![WhatsApp Image 2025-11-20 at 1 10 41 PM](https://github.com/user-attachments/assets/ee367c96-e7fb-49b9-bff2-2d8452db7f07)

## OUTPUT

![WhatsApp Image 2025-11-20 at 1 58 44 PM](https://github.com/user-attachments/assets/bf554d68-7b51-4e7f-a103-55032f8a1937)

## RESULT
Thus the frequency modulation and demodulation is successfully done and the output is experimentally verified.
