# UlisseCTF 2025 - Forensics
## AWAWA
![image](https://hackmd.io/_uploads/B1HuVSxAJg.png)

This challage gave me a .jpg file. 
![image](https://hackmd.io/_uploads/SyLhEHlCkg.png)
Everything looked unsuspicous.

Also nothing with `exiftool`
![image](https://hackmd.io/_uploads/B1syBrxA1l.png)

`foremost` and `binwalk` also had nothing to extract :cry: 
![image](https://hackmd.io/_uploads/BkvmBBgRye.png)

Let's try `steghide`. First time, I looked at description and thought that "AWAWA." was the passphrase but it not :cry: 
![image](https://hackmd.io/_uploads/SyVtrHgAke.png)

Then, I tried with no passphrase and it worked. The description made me confused.
![image](https://hackmd.io/_uploads/HkMCSBxCyg.png)

So, we have the wav file. Let's open it with `Audacity` and use `Spectrogram` for the flag
![image](https://hackmd.io/_uploads/Hk_NIreR1x.png)

**FLAG: UlisseCTF{St3g0_M4st3r}**


## Internet of Lighthouse
![image](https://hackmd.io/_uploads/BySgwNxRke.png)

This challenge gave me a pcap file. Let's open it with Wireshark

![image](https://hackmd.io/_uploads/H1hUPNlAkg.png)

It has TCP and HTTP/JSON protocol, I checked TCP streams

![image](https://hackmd.io/_uploads/H10KDNeA1x.png)

It contains 67 streams, and the differences are the `timestamp` and `onoff`. First, I checked the `onoff`, it changed between `0` and `1`. So I thought it like a binary string, and extracted it from 67 streams.

`1001011011011110101110110000100010101110010010011111111011101111101`

Convert it to ASCII but nothing happens. So I paid attention to `timestamp`. I realized that some adjacent streams had same `timestamp`, it was bettwen 1 -> 4 adjacent streams, so It could basically be Morse code.

So I splited it into the cluster with same `timestamp`, 1 is `.`, 0 is `-`

The result:
```
.-- .- .. - .. - ... .- .-.. .- .. -- --.- - - .- .-.. .-- .- -.-- ... .... .- ... -... . . -.
```

I decoded it, ya saw some English words but not all correct.
"WAITITS" and "ALWAYSHASBEEN" maybe is correct.
![image](https://hackmd.io/_uploads/SygqFEg0yl.png)

Hmm, the division was not correct somewhere in the middle, I checked again with `timestamp`, sometimes it increased `5` but sometimes it just increased `1` (There only one bruh). I focused on the time changed `5`, if the timestamp difference is none or `1`, it didn't push any " ", else pushed " ".

So the result changed a little bit in the middle.

![image](https://hackmd.io/_uploads/S1VVMrl0Je.png)

**FLAG: UlisseCTF{WAITITSALLMQTTALWAYSHASBEEN}**


