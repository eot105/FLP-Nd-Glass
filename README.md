# FLP-Nd-Glass: Homebrew flashlamp pumped solid-state Nd:Glass LASER.

<figure>
<center><img src="Resource/full_system.JPG" style="width:50%" style="height:50%" class="center"></center>
<figcaption align="center"><b>Fig 1. Full laser system showing the pump head, rod, flashtube, trigger circuit and various optics.</b></figcaption>
</figure>

This project was completed in Aug of 2021. The result of 3 years of research, experimentation, failure, and learning. 

The first coherent photons were observed around 10pm on Aug 8th 2021 in a friend's lake house outside of Syracuse NY where I was staying over the summer (Thanks Christy, for not kicking me out when you found a laser in your living room). The first shot was a barely visible mark on a piece of laser alignment paper. Over the following days, with more tuning and alignment I was able to extract what was likely the maximum output of the laser given the flashtube and caps I have access to. When focused, the beam has no issue passing the standard test for homebrew lasers, burning through a carbon steel razor blade. 

<figure>
<center><img src="Resource/washer_shot_sparks.png" style="width:50%" style="height:50%" class="center"></center>
<figcaption align="center"><b>Fig 1. Beam focused onto a stainless steel washer.</b></figcaption>
</figure>

The laser rod is surplus soviet era neodymium doped silicate glass marked "GLS-1" with an [Nd<sup>3+</sup>] concentration of 1.9 * 10<sup>20</sup> cm<sup>-3</sup> (about 2%). This rod was an e-bay find and was re-machined by the seller, supposedly by a professional optics shop. I have no way of verifying the precision of the rod, but it did lase in the end so I will take the sellers word for it. This refinishing left the rod with a odd size of 11mm by 92mm. 

Partly owing to this non standard size, the rod was housed in a custom machined elliptical chamber. The design consisted of two parts, the clamshell style pump head that held the rod and flashlamp at the two foci of an ellipse, and a baseplate that held the pump head and mirrors in place. The parts were custom machined out of 6061 aluminum and the inside of the pump head was polished to a mirror finish to give the best optical coupling.

<figure>
<center><img src="Resource/mirror.png" style="width:50%" style="height:50%" class="center"></center>
<figcaption align="center"><b>Fig 2. Polished pump head.</b></figcaption>
</figure>

The flashlamp used for the laser went through several iterations. Quartz xenon flashtube have several emission peaks that correspond well to the absorbance peaks of the Nd<sup>3+</sup> ion in the laser rod. I stated with a soviet era tube about the same vintage as the rod (the IFP-800) there is some info on this tube at [Don Klipstein's flash lamp page](http://donklipstein.com/xea.html). I had an awful time getting this tube to work, the seals on the glass are dated and prone to cracking. In addition this tube is almost comically long compared to the active region, which meant the baseplate had to be a much longer than was needed. This also brought the ends of the tube too close to the mirror mounts resulting in some nasty arcing problems. Some of these tubes (mine included) have a dichroic coating on the outside of the glass meant to cut off the UV-C portion of their output. This seemed at first like a good thing, but ended up causing the most catastrophic accident that this project saw. Because I am using an external triggering scheme, the trigger pulse would often arc across the conductive dichroic coating rather than couple into the glass and start the arc. Each time this happened the glass was left with a hairline imperfection. One night, while experimenting with ways to mitigate this problem, the tube violently exploded. Had the tube not been inside the pump head this would likely have been an injury inducing accident, and served as a fierce reminder as to just how much energy even a modest laser system like this one can deliver.

<figure>
<center><img src="Resource/tube_explode_1.png" style="width:50%" style="height:50%" class="center"></center>
<figcaption align="center"><b>Fig 2. Aftermath of the flashtube explosion.</b></figcaption>
</figure>

Needless to say the IFP-800 left a bad taste of ozone and glass shrapnel in my mouth. I was lucky to find a different tube of domestic origin, and made in the last 20 years, on e-bay: the EM1019 from [Fenix Technology](https://www.fenixtechnology.com/showflash.html). This tube was almost exactly the same diameter and had almost exactly the same active length as the previous one, so I could use my pump head un-modified. The triggering was still an issue. The lamp needs about a 20kV pulse to trigger, and pulses at voltages that high have a habit of finding creative paths to ground, regardless of any attempts to insulate the pump head from the rest of the system. The solution that ended up working was wrapping a thin nickle wire around the active length of the tube and feeding it through a nylon bolt that I threaded through the side of the pump head. This kept the high voltage away from the metal body and eliminated the arcing problem. 

<figure>
<center><img src="Resource/trigger_wire.png" style="width:50%" style="height:50%" class="center"></center>
<figcaption align="center"><b>Fig 2. New flashtube with trigger wire.</b></figcaption>
</figure>

<figure>
<center><img src="Resource/trigger_bolt.png" style="width:50%" style="height:50%" class="center"></center>
<figcaption align="center"><b>Fig 2. Trigger wire with insulating nylon bolt.</b></figcaption>
</figure>

The trigger circuit consists of a 300V electrolytic cap meant for photoflash applications, connected via a high voltage SCR across an automotive ignition coil which is essentially an oil filled transformer with an 80:1 turns ratio. This should give a pluse of 24kV on the output. This pulse is applied directly to the outside of the tube, where it is capacitively coupled to the electrodes creating a low resistance path that the main cap bank can discharge across, resulting in a flash. The 300V cap is charged with an off the shelf high voltage flyback converter powered from a 12V wall wart. The whole trigger circuit is contained in a plastic box with a high voltage connector and well insulated alligator clip for connection to the trigger wire. 

<figure>
<center><img src="Resource/trigger_circuit.png" style="width:50%" style="height:50%" class="center"></center>
<figcaption align="center"><b>Fig 2. Trigger circuit contained in ABS enclosure.</b></figcaption>
</figure>

The fluorescence lifetime of the Nd<sup>3+</sup> ion in the laser rod is 450&mu;s. This is the mean time between when the ion is moved to its excited state by absorbing a photon and when it emits another photon by falling back down to its ground state. In order to achieve a population inversion, a majority of the ions in the rod must be brought into the excited state during a given instance of time. If the pulse delivered to the rod is longer than the fluorescence lifetime of the ion, the ions will start to decay before a population inversion is achieved. There is some wiggle room here: the fluorescence lifetime of the ion is an average, and the pulse of light from the tube is not rectangular, there will be some "fade in" and "fade out" as it fires. What this means is that I can target a slightly longer pluse time than would be expected from the fluorescence lifetime of the ion, which makes building the circuit somewhat easier. In this case I shot for a pulse time of 500&mu;s. To get a pulse this short electrolytic capacitors can not be used, their internal inductance is too high. Polymer film caps are the gold standard for this application. I was lucky enough to find a crop of 8 UL30BF0290 750V 290&mu;F caps on e-bay. I placed 4 of these in parallel to get a capacitance of 1,160&mu;F and then placed two banks in series to get a maximum voltage rating of 1500 while halving the total capacitance down to 580&mu;F. This gives me a maximum energy storage of 652J. In operation I only ever charged the bank to 1150V, which limited the maximum energy to 383J. At a pulse width of 500&mu;s this operates the tube at 22.44% of its "explosion energy" and should result in a lifetime of over 100,000 flashes.

<figure>
<center><img src="Resource/cap_bank_2.png" style="width:50%" style="height:50%" class="center"></center>
<figcaption align="center"><b>Fig 2. Main capacitor bank.</b></figcaption>
</figure>

In order to tune the system to get the correct pulse length a series inductor is added between the bank and the flashtube to lengthen the pulse time. The value of this inductor is found given the desired pulse length, total energy in the bank, and some properties of the flashtube. Using this [calculator](https://www.fenixtechnology.com/fenixcalc.html), the needed inductor was found to be 47.89&mu;H. I made one using a large ferrite toroid and a few turns of solid core 12AWG wire.

Charging this cap bank was another aspect of the project that went through several iterations. I tried at first to use an electrophoresis power supply. These are awesome as you can set them in constant voltage, current or power modes, and they are the safest method available to most enthusiasts to charge high voltage cap banks. Unfortunately they are expensive and finding models that go much higher than 600V is difficult on the second hand market. A more practical, but much less safe, option is to use a neon sign transformer (NST) hooked up to mains voltage and a high voltage diode to rectify the output. For these applications you need an old school NST thats basically just a high turns ratio transformer, the new high frequency digital NSTs will not work for cap chargers. Old style NSTs can still be found on ebay, though in deceasing numbers. The smallest NST I could find was one that gave 3500V output at 120V input. To regulate the output down to the ~1.1kV I need for the cap bank I run the mains voltage through a variac before the input of the NST. This also gives some marginal increase in safety as I can slowly increase the voltage applied to the bank and creep up on the target voltage. The output of the NST is rectified through a single 5kV diode. To measure the voltage across the bank I used a 3kV analog panel meter.

<figure>
<center><img src="Resource/NST.png" style="width:50%" style="height:50%" class="center"></center>
<figcaption align="center"><b>Fig 2. Neon sign transformer used to charge main cap bank.</b></figcaption>
</figure>

The optics for this laser were all purchased from a chinese company called [master laser](https://master-laser.cn/). The mirrors (both full reflect and output coupler) I purchased are high performance dichroic types tuned for the ~1064nm light an Nd:Glass laser produces. It is unlikely that at these modest output powers such mirrors are necessary or offer any real benefits. Sam Goldwasser's [laser blog](http://www.repairfaq.org/sam/lasercps.htm#cpstoc) states that a myriad of less than optimal mirrors have yielded success in these homebrew style systems, form polished pennies used for full reflects and stacks of microscope slides used for output couplers. Nonetheless it is nice to eliminate the variable of the optics from an otherwise variable ridden project. The mirrors are held in standard kinematic mirror mounts typically used in CO<sub>2</sub> laser cutters.

The focus lense was purchased from the same company, a similarly wavelength specific dichroic coated positive focal length lense with an inconveniently long focal length of 110mm. The lens was "mounted" even less precisely than the mirrors using a piece of wire and small alligator clip vice, which proved to be fine for what I needed. 

To align the cavity I used a commercial He:Ne laser mounted on a tripod and a piece of white paper. My mirrors are thick pieces of glass, partially reflective to the visible light of the alignment laser. Because of this there are multiple reflections off the front and back of the mirrors, which combined with the suboptimal mirror mounds makes aligning this laser very difficult, but with some screwing around it's possible to get it aligned well enough for a successful shot.

This "Zap-It" paper proved to be a very useful tool in determining how well the cavity was aligned, and this side by side shows how sensitive the system is to this variable. 

<figure>
<center><img src="Resource/weak_shot.JPG" style="width:50%" style="height:50%" class="center"></center>
<figcaption align="center"><b>Fig 2. Barely visible marks left by a poorly aligned cavity.</b></figcaption>
</figure>

<figure>
<center><img src="Resource/strong_shot.JPG" style="width:50%" style="height:50%" class="center"></center>
<figcaption align="center"><b>Fig 2. Much stronger shot left by a better aligned cavity.</b></figcaption>
</figure>

It took the better part of 3 years to get this laser working, and there are still plenty of improvements that could be made. Maybe I will revisit this in the future, maybe not. Regardless, the idea was more to explore the science, and the knowledge and skills that I gained in a diverse set of felids while working on this project is really the reason that us hobbyists take on things like this.

<figure>
<center><img src="Resource/razor_shot_sparks.png" style="width:50%" style="height:50%" class="center"></center>
<figcaption align="center"><b>Fig 2. Laser burning a hole in a razor blade.</b></figcaption>
</figure>

<figure>
<center><img src="Resource/Razor Shot Clip.gif" style="width:50%" style="height:50%" class="center"></center>
<figcaption align="center"><b>Fig 2. Laser burning a hole in a razor blade.</b></figcaption>
</figure>
