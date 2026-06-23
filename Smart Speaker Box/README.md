Smart Speaker Box

Due to limitations in ESP hardware it is not possible to have more than 2 I2S devices connected.  One of these has to be the microphone and as a result only 1 channel can be used for DACs to allow output.

In order to get past this limitation both DACs are connected to the same pins on the ESP and they are individually muted depending on requirements.  Media playback goes via the PCM 3.5mm dac and TTS / announcements are routed via the MAX and internal 2" speaker.

There are some limitations to this setup.  Media is streamed to the device and uses the built in mixer system to queue playback.  TTS / Announce is given priority, which means it will interupt media playback and then media playback will resume.  There are however multiple buffers in the audio stream, their exact size is variable and there is no flag for when the buffers exhaust. As such you will get media output via the 2" internal speaker for a period before the TTS starts.  This ranges from sub 50ms to a second.  I have not been able to find a solution to this.  There is occasionally a small pop at the end of TTS before it switches back to the PCM.

The design setup is intended for 100% volume on both DACs.  This is a suitable volume level for the TTS output.  Adding it as a variable will likely happen in the future.

Finally SendSpin is very CPU intensive, you need to specify that the player receives PCM output from MusicAssistant otherwise CPU will get overwhelmed and you will lose wakeword detection.  There is occasional audio corruption when playback first starts, transient for up to 2 seconds.  This is all caused by CPU bind.  
