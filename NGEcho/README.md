# NGEcho.amxd
![NGEcho.amxd](https://github.com/noelalejandro/Max/blob/main/assets/NGEcho.amxd.png)
###### Video Demo Coming Soon!

#### [NGEcho.amxd](https://github.com/noelalejandro/Max/blob/main/NGEcho/NGEcho.amxd) is a Feedback Delay Network (FDN) Echo Machine & Reverberator, designed and programmed for use in Ableton Live Suite. Drawing upon the legacy of digital signal processing pioneers Manfred Schroeder, Ben Logan, John Stautner, and Miller Puckette, NGEcho.amxd is capable of simulating warbly tape echoes or lush reverbs with infinite decay. Users have control over:
- Input/Output gain
- Pre-Delay
- Delay Time in two modes: Free (ms) & Sync (bpm)
- Feedback
- Blend which smoothens out transients
- Lo Cut/Hi Cut/Q of a State Variable Filter on the device's output
- Dry/Wet mix amount

#### In its current form, NGEcho.amxd is strictly for use in Ableton Live Suite though, in later iterations, I intend to implement the device as a VST3 & AU component. As a proof of concept, I have created them as VST3 & AU using Max's RNBO Audio Plugin Export functionality. A basic plugin is created using the JUCE framework but the GUI leaves much to be desired. My intention is to develop the programming skills required to improve upon this user interactivity and interface. 

## Install NGEcho.amxd

1. Follow the link to the [NGEcho.amxd](https://github.com/noelalejandro/Max/blob/main/NGEcho/NGEcho.amxd) repository
2. Download raw file
3. Place .amxd file in the Devices folder of your Ableton User Library
4. Navigate to the Max For Live tab in your Ableton Live browser window, the device should populate in the Max Audio Effect folder

## Background
####
My goal with this research was to develop a reverb plugin that would be utilized by musicians for dynamic performance and sound design, and by academics interested in learning the basics of digital reverb algorithms. This project stems from my desire to understand digital signal processing on a deeper level, and to develop tools for artists to use in their creative endeavors. The desire to focus on reverberation came primarily from my own experience using these types of plugins in the digital music domain, and witnessing how certain aspects of reverb, when modulated, introduced artifacts into the audio signal. Often when adjusting room size, a reverb plugin would crackle or pop. This is an unwanted byproduct of certain designs. My aim was to develop a digital reverb plugin that is performable, responsive, and endlessly malleable without causing these artifacts. The result is more along the lines of an echo device that is capable of procuding lush reverbs, but is also capable of much more. 

## A Breif History of Digital Reverberation
####
Early pioneers of digital reverberation include Manfred Schroeder and Ben Logan who, in 1962, designed an artificial reverb that consisted of a series of allpass filters and a parallel bank of comb filters. In this early topology, four feedback comb filters are followed by three allpass filters which add complexity to the primary echoes, or early reflections, of the comb filters. The result is a smearing of the original sound. It’s a very primitive design, and not entirely convincing as a reverb as it doesn’t quite emulate a room or a concert hall. James Moorer expanded on this design by introducing lowpass filters within the parallel bank of comb filters. By doing so, he was able to approximate more accurately the propagation of sound in a room by dampening the higher frequencies over time. Moorer also introduced a finite impulse response (FIR) filter with several delay taps to approximate the early reflections in a room. This adds a good amount of complexity compared to the Schroeder reverb design. 

In 1977, Christopher Moore left Lexicon to start his own company called Ursa Major. He developed a complex single feedback delay line with twenty-four taps, and slowly modulated and randomized the time of each one. This effectively increases the echo density and adds even more complexity upon each recursion through the network. In 1982, John Stautner & Miller Puckette devised a delay line feedback matrix based on the Hadamard matrix. The innovation that was introduced with this design was a unity gain feedback matrix, meaning the reverb could be sustained infinitely. This was not possible with the previous reverb topologies. David Griesenger, another key engineer at Lexicon, introduced a figure-8 feedback loop with modulated allpass filters nested between each delay line. Over each recursion of the loop, echoes become more complex and subtle phasing introduced. 

## Tools
####
Drawing inspiration from these topologies, I planned to create a reverb that is variable in its echo density, coloration, diffusion of early reflections, with a smooth exponential decay. The tool I chose to undertake this project was Max 8. Max is a visual programming language that is used by composers, performers, software designers, researchers, and artists to develop customizable tools for any given purpose. Within the Max patching environment, there is an object called Gen~ that allows for the combination of procedural commands with visual programming. Gen~ addresses audio signals on a single-sample basis, rather than in vector buffers, making it much more efficient than the standard MSP objects. Gen~, as well as RNBO~, compiles C++ code as you work and this code can be exported to create VST, AU, and iOS applications.

## Design Process
####
My process began with research: I poured over Julius O. Smith's ["Physical Audio Signal Processing"](https://ccrma.stanford.edu/~jos/pasp/), specifically the sections on Allpass Filters, Feedback Delay Networks (FDN), and the Tapped Delay Line (TDL). These are the essential building blocks of digital reverberation algorithms, and I wanted to understand the math and science behind how they work. I implemented an [Allpass Filter](https://github.com/noelalejandro/Max/blob/main/assets/NGEcho/ap_diagram.png) from two Comb Filters in Max using the Gen~ operator.

<img src="https://github.com/noelalejandro/Max/blob/main/assets/NGEcho/ap.png" width="50%" height="50%">

I encapsulated this bit of code, named "gen ap", to be able to duplicate it easily. I then created a chain of five Allpass Filters.

<img src="https://github.com/noelalejandro/Max/blob/main/assets/NGEcho/apchain.png" width="50%" height="50%">

Here you can see that the delay line lengths are mutually prime and span successive orders. This is done in order to minimize the overlap of their frequency responses, to inhibit the build up of resonance and beating. The delay time is also being modulated by an lfo.

I continued by looking into Stautner' & Puckette's FDN design. A essential component of any FDN is its matrix. There are various matrices that have been implemented in different reverb designs but I chose to include a [4x4 Hadamard Matrix](https://github.com/noelalejandro/Max/blob/main/assets/NGEcho/hadamard_matrix.png), as shown below.

<img src="https://github.com/noelalejandro/Max/blob/main/assets/NGEcho/hadamard.png" width="50%" height="50%">

I then began to assemble the Input, FDN, and Output sections.

<img src="https://github.com/noelalejandro/Max/blob/main/assets/NGEcho/input.png" width="50%" height="50%">
<img src="https://github.com/noelalejandro/Max/blob/main/assets/NGEcho/output.png" width="50%" height="50%">

#### Alpha Test
I used various forms of social media to reach out to musicians, colleagues, and anyone interested in trying out the device in order to provide feedback that I could use to improve upon its design. I received messages an astounding 30 volunteers and sent an email with the device attached. I didn't want to set too many parameters for their exploration, but I did ask for some specific feedback:

How does it sound? Do the parameters make sense? What does it lack? What could be omitted?

The responses were positive, and many users wanted implementations that I had not considered. Most agreed that it acted more as an echo device that could emulate a reverb. So of the improvements and modifications, the most common were:

- Tempo sync with subdivisions
- Possibility of shorter delay times for flanger-like effects
- Low Cut and High Cut filters with variable resonance

#### Re-Iterate
The tempo sync functionality was tricky to implement. I had to figure out a way to switch the Time knob from milliseconds to subdivisions of the transport clock in Ableton. This required duplicating the knob, changing its values and range, and figuring out how to hide one while the other was visible. 

<img src="https://github.com/noelalejandro/Max/blob/main/assets/NGEcho/controlmode.png" width="50%" height="50%">

## References
###### [1] [Cycling '74 Max 8 Documentation](https://docs.cycling74.com/max8)
###### [2] [Cycling '74 Forums](https://cycling74.com/forums/page/1)
###### [3] [Cycling ‘74 YouTube - “Max For Live Best Practices” Tutorial](https://youtu.be/7mk4JMBVDZ4)
###### [4] ["Physical Audio Signal Processing" - Julius O. Smith III](https://ccrma.stanford.edu/~jos/pasp/)
###### [5] ["The Theory And Technique Of Electronic Music" - Miller Puckette](http://msp.ucsd.edu/techniques/latest/book.pdf)
###### [6] ["Musical Applications Of Microprocessors" - Hal Chamberlin](http://sites.music.columbia.edu/cmc/courses/g6610/fall2016/week8/Musical_Applications_of_Microprocessors-Charmberlin.pdf)
###### [7] ["Building The Erbe Verb" - Tom Erbe](https://quod.lib.umich.edu/cgi/p/pod/dod-idx/building-the-erbe-verb-extending-the-feedback-delay-network.pdf?c=icmc;idno=bbp2372.2015.054;format=pdf)
