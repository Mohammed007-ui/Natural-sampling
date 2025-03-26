# Natural-Sampling
## Aim:
To perform natural sampling by multiplying a message signal with a pulse train. To analyze the sampled signal and observe its reconstruction.
## Tools required: 
+ Personal Computer with Scilab
+ Python IDE (Numpy)
## Program: 
~~~
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import resample

# Define message signal (low-frequency signal)
fs = 1000  # High sampling rate to represent original signal
t = np.arange(0, 1, 1/fs)
fm = 2  # Message signal frequency
message_signal = np.sin(2 * np.pi * fm * t)  # Message signal

# Define pulse train for natural sampling
fs_sampled = 20  # Sampling frequency
duty_cycle = 0.3  # Duty cycle of pulse (30% width)
pulse_train = np.zeros_like(t)
pulse_width = int(duty_cycle * (fs / fs_sampled))

# Generate pulse train
for i in range(0, len(t), fs // fs_sampled):
    pulse_train[i:i + pulse_width] = 1

# Natural sampled signal (Message signal × Pulse train)
sampled_signal = message_signal * pulse_train

# Reconstruction using sinc interpolation
reconstructed_signal = resample(sampled_signal, len(t))

# Plot Message Signal
plt.figure(figsize=(10, 5))
plt.plot(t, message_signal, label="Original Message Signal", color='b')
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.title("Message Signal")
plt.legend()
plt.grid()
plt.show()

# Plot Natural Sampling
plt.figure(figsize=(10, 5))
plt.plot(t, message_signal, linestyle="dashed", alpha=0.7, label="Original Signal")
plt.plot(t, sampled_signal, 'r', label="Naturally Sampled Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.title("Natural Sampling of Message Signal")
plt.legend()
plt.grid()
plt.show()

# Plot Reconstructed Signal
plt.figure(figsize=(10, 5))
plt.plot(t, message_signal, linestyle="dashed", alpha=0.7, label="Original Signal")
plt.plot(t, reconstructed_signal, 'g', label="Reconstructed Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.title("Reconstruction from Natural Sampling")
plt.legend()
plt.grid()
plt.show()
~~~
## Output Waveform:
![image](https://github.com/user-attachments/assets/a5b72b49-8917-4990-8e1e-d78202a9d1b0)

![image](https://github.com/user-attachments/assets/6e4e1a67-0165-4d94-854b-360369ea4827)

![image](https://github.com/user-attachments/assets/a91c7a4c-c571-4f45-936a-26a043d54bfc)


## Results:
Natural sampling was successfully performed by modulating the message signal with a pulse train. The reconstruction process demonstrated that a higher duty cycle improves signal recovery, while a lower duty cycle leads to distortion.
