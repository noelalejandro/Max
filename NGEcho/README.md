# NGEcho.amxd
[![NGEcho.amxd](https://github.com/noelalejandro/Max/blob/main/assets/NGEcho.amxd.png)](youtubelink)
###### Click Image To Watch Demo

#### [NGEcho.amxd](https://github.com/noelalejandro/Max/blob/main/Rhodonea/Rhodonea.amxd) is an Feedback Delay Network (FDN) Echo Machine & Reverberator, deisgned and programmed for use in Ableton Live Suite. Drawing upon the legacy of digital signal processing pioneers Manfred Schroeder, Ben Logan, John Stautner, and Miller Puckette, NGEcho.amxd is capable of simulating warbly tape echoes, lush reverbs, and infinite decay. Users have control over:
- Input/Output Gain
- Pre-Delay
- Delay Time in two modes: Free(ms) & Sync(bpm)
- Feedback
- Blend which smoothens out transients
- Lo Cut, Hi Cut, & Q on 

#### In its current form, Rhodonea.amxd automatically takes an audio signal input to modulate RGB values. In later Iterations, I hope to implement an auto/manual toggle for complete control over color output. This device is a derivative of code by [Umut Eldem](https://github.com/umutreldem/hearing-glass/tree/main/tutorials), licensed under GNU General Public LIcense v3 (GPL 3.0).

## Install NGEcho.amxd

1. Follow the link to the [NGEcho.amxd](https://github.com/noelalejandro/Max/blob/main/NGEcho/NGEcho.amxd) repository
2. Download raw file
3. Place device in the Devices folder of your Ableton User Library


## Design Process
#### Learn
Having never programmed anything in Max, I spent hours reading over bits of the Max 8 documentation. Cycling '74 has done an amazing job with their documentation by providing extensive tutorials and guides on Max, MSP, and Jitter. The Max community forum also offers great support and feedback on projects, which anyone learning would find super useful. The YouTube tutorials were instrumental in figuring out what was going on inside the world of Max and, since this project is of an audio-visual nature, much of my time was spent watching Jitter tutorials. Jitter handles all of the visual processing, transformations of matrices, and handling of complex data structures for storing video. 
#### Refine
What intriguiged me most, at first, were abstract visuals - not necessarily generating specific images, or even an audio visualization tool. I was looking at work by artists like [Gleix](http://gleix.net/visualdevices), who operate primarily in the realm of analog visual synthesis. After being introduced to [Oscilloscope Music](https://oscilloscopemusic.com/maxforlive.php) by Dr. Daniel Dehaan, I began to develop an interest in creating a Max patch to be able to "draw" with sound. Realizing that this was outside the scope of a short term project, I decided to stick with a simple Max for Live device: an audio-reactive visualizer.
#### Iterate
Following the tutorial by Umut Eldem, I was able to get the patch operating rather quickly. More time was spent seeing how far I could take that basic patch - which parameters could be modulated, what worked well vs. what didn't. I ended up with ten parameters that could all be modulated, assigned to lfo's, shapers, eveloe followers, etc.
#### Package
Once I was satisfied with the device and the visuals it produced, I watched Cycling '74's "Max for Live Best Practices" tutorial via their YouTube channel. This was very helpful in making sure that the device would appear just like any other device in Ableton. From encapsulation to documentation, this tutorial offers in-depth analysis of a proper Max for Live device. The inner workings of Rhodonea.amxd serve as a testament to this incredibly useful resource.
#### Beta Test
The final step in development was the Beta Test. I sent Rhodonea.amxd to colleagues and friends for comments and feedback. Only in one case did the device not work at all - but this may have been due to the fact that the user was working with a cracked copy of Ableton Live Suite. The others had only nice things to say and offered helpful suggestions on how to improve upon the device.


## References
###### [1] [Max 8 Documentation](https://docs.cycling74.com/max8)
###### [2] [Cycling '74 Forums](https://cycling74.com/forums/page/1)
###### [3] [Cycling ‘74 YouTube - “Max for Live Best Practices” Tutorial](https://youtu.be/7mk4JMBVDZ4)
###### [4] [Oscilloscope Music - Max for Live Patches](https://oscilloscopemusic.com/maxforlive.php)
###### [5] [Hearing Glass (Umut Eldem) YouTube - “Polar Rose with jit.gen” Tutorial](https://youtu.be/PDrfcPgnhSA)
###### [6] [Amazing Max Stuff YouTube](https://www.youtube.com/c/AmazingMaxStuff)
