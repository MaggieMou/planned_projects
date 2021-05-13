# Planned Projects
Here is a list of upcoming plugins and applications. If you want to add things, please make a new issue.
At the top of the list are the "coming soon" descriptions of plugins I am currently working on,
below that is a brainstorm of plugin ideas that have been suggested or that I am curious to try,
but which are not currently in development. The coming soon section is in order of which one
is most likely to come out first.

## Coming Soon: VIBE_MACHINE (name might change) - instant vaporwave/plunderfonics-ifyer effect
***Commissioned by Synes*** - ***Almost complete!***

VIBE_MACHINE is a badly behaved delay plugin, where the input is passed through three
different delay lines, left, mid and right, each one is controlled by the same "length"
knob, but has a different irrational proportion of whatever the "length" knob shows, so
that it is futile to try and sync it with the project's tempo. This is very intentional,
as it makes it sound quite granular.

Additionally, each delay line has a playback speed which can be chosen from a list of
musical combinations, and which affects the pitch of each delay line, creating shimmer-like
effects, and making any attempt of syncing with the project tempo even harder.

Within the feedback path of each delay line are: a tape wow kind of vibrato, saturation
and diffusion. This quickly turns the delay into more of a granular smear of harmonics.

As a twist, every control has obscure names so that you stop thinking technically and
start actually listening to what you are doing, this feature can be disabled if you
are a boring person.

## Coming Soon: NON_LINEAR_FILTERS - bunch of non-linear filters for testing purposes
This is another "meta-plugin" like HYSERESIS. Not really a finished product, but a 
showcase of some of the technology that I am developing for the purpose of building
larger plugins in the future.

Non-linear filters have interesting properties that make them less usable for 
technical applications, but more fun for creative applications. They don't have the
same frequency response for all levels of input loudness and/or they distort the
signal, adding harmonics additively.

This one is very simple, it has three knobs: mode, lp/hp mix, cutoff
- mode selects the type of filter, these are not necessarily related to each other
  - 2-pole Airwindows Capacitor2-esque filter
  - 4-pole ariwindows filter
  - soft first order slew clipper (formerly "erase" knob on hysteresis)
  - soft second order slew clipper
  - hard first order slew clipper
  - hard second order slew clipper
  - first order median filter
  - second order median filter
  - logarithmic 2-pole biquad: takes the log of the signal, filters it, then takes the exponential
  - logarithmic 4-pole biquad
- lp/hp mix: crossfades between lowpass mode and highpass mode, in between there is something like a notch or similar
- cutoff: approximate cutoff of the filter, this cannot possibly be precise because non-linear filters have different
  frequency responses at different levels of the input


## Coming Soon: POWER_OF_THE_BATHROOM - Room reverb and distortion, can self-oscillate
A simple room reverb, with a twist: there's distortion in the feedback path.
Drive it to create electric guitar-esque overdrive and cab like sounds. There is
some inaudible white noise added to the input, so that when the feedback is above
unity gain, it goes into self-oscillation, producing harsh metallic drones.

The name comes from the fact that it sounds like a bathroom reverb, and that it also
makes for some good power electronics / harsh noise.


## Coming Soon: BUFFER_FUCK \ BUFFER_THRASHER- audio buffer corruption effect.
***planning stage***
The incoming audio is pushed into a buffer (a sort of digital equivalent to a piece of
audio tape). Then various operations are performed on the buffer to mangle it:

- Input to index-FM: the position of the read index in the buffer is modulated by the
  input.
- Output to index-FM: the position of the read index in the buffer is modulated by the
  output of the plugin, this introduces a feedback dependency, which I expect will
  sound cool.
- Terrible pitch shifting: the read index is moved at a constant speed to produce a
  very bad pitch shift effect.
- Scrape flutter: the read index is moved around at random, producing heavy side-band
  distortion.
- Buffer freezing: the output is fed back into the input, crossfaded with the dry input,
  so at 100% feedback, there is no new input being placed into the buffer, essentially
  freezing it, getting more and more mangled.

## Coming Soon: MIKROSYN - lo-fi phase distortion monosynth
***Commissioned by Bjarke*** - ***planning stage***
MIKROSYN is in the planning phase, where is the plan? You are reading it right now.

MIKROSYN is a phase distortion monosynth, i.e. there is a ramp oscillator at its core,
constantly outputting a *phase* that is then shaped to produce all the basic shapes:
- Triangle shaper with asymmetry control: changes the slope of the rising and falling
  edges so that it varies continuously between triangle and saw wave.
- Pulse shaper with PWM control: turns the ramp into a pulse, the PWM has LFO control
- Sine shaper: turns ramp into a sine, can be pushed past 100% to sound like a hard-synced 
  sine wave.
- Noise: crossfade between the oscillator and pink noise, to mix in a bit of dust.
So far, if we were to take each shaper in parallel, we would have the classic design
of an analog multimode oscillator, albeit a bit more buchla style than what the plugin
world is used to; however what makes this interesting is that I've broken it. 

Each shaper has now a continuous
variable "amount" parameter, so you can get an in-between shape, between saw and 
whatever shape that specific shaper is doing. Another way this is broken, is that
all these shapers can be active at the same time, chained together, for interesting
results. Even more interesting, is that the noise parameter is introduced before
all the shaping, so it gets mangled and chewed up together with the phase.

Additionnally, there is a "unison" amount knob, this duplicates the phase ramp into
multiple detuned phase ramps, which are summed together *before* the shapers, making
a lot of fun dissonant distortion.

Finally, everything is encoded into 6-bit mu-law format, with limited sample rate. The
sample rate can either be fixed, acting like a bit-crush, or it kan be keyboard tracking,
meaning it can be tuned to created intervals. The 6-bit encoding is heavily lo-fi and
can be turned off if unwanted.

After this digital section, there is a gentle analog-ish low-pass-gate to tame some of
the high end. The LPG is controlled by an AD / AR envelope. Alternatively, the envelope
can be routed to the sine shaper instead, and the LPG is fixed at a set level. This
makes the synth sound very Buchla-esque, especially when pushing the sine shaper.

The oscillator section of this may or may not become a Eurorack module in the future.

## STOCHASTIC - Stochastic bitcrusher
STOCHASTIC can both be a normal bitcrusher, and what I call a "stochastic quantizer".
- A bitcrusher samples the incoming sound at a regular rate, lower rate than the host 
  sample rate, producing heavy intentional aliasing distortion.
- A stochastic quantizer, samples the input, and only samples it again based on probability,
  the more the input differs from the sampled value, the higher the probability. This is
  similar to how objects move when they are pushed lightly and they have to overcome friction,
  moving at irregular steps once pressure accumulates enough to win the friction.
In between these two effects is a space of in-between effects controller by three parameters:
- Rate: how often the input is sampled per second.
- Regularity: turns the effect from a probabilistic mode, where rate controls the probability
  rather than the pure rate of the samples, to a deterministic rate, where the rate control
  dictates precisely how often the input is sampled.
- Input-dependence: goes from the samples being triggered invariantly of the level of the input,
  to the samples being triggered when the difference between the held value and the input is large enough,
  again, when the process is probabilistic, the difference is a probability, when it is deterministic,
  the difference triggers a sample at a fixed threshold.


## Coming Soon: GRAINTABLE (name might change) - Granular wavetable polysynth
***Commissioned by Plebber*** - ***planning stage***

GRAINTABLE is a cross between a granular synth and a wavetable synth. Essentially
each grain is a tiny little synth instance, that plays a short note, with variable
attack, sustain and release, and then ceases to exist. Each grain plays from a
wavetable, the wavetable position can be set by a master control, then randomized
for each individual grain, additionally each grain might scan the table at a separate
speed and might have a randomized pitch.

The wavetable selection is built-in because a fully-featured wavetable editor is way
past my skill level. I'm thinking a minimalistic mix of utilitarian wavetables, arranged
in an X-Y-Z single wavetable bank, so that they can be scanned tangentially.

## Coming Soon: CASSETTE - Lo-fi cassette emulation
- Low quality input transformers
- Low quality transistor amplifiers
- Tape correction EQ (pre and post)
- Various modes of noise reduction compression and EQ, based on dolby NR, and dbx. Also
  emulates the mismatch of encoding and decoding noise reduction methods.
- Tape saturation and hysteresis
- Realistic hiss from electronic thermal noise and tape grain
- Wow, flutter and scrape flutter

## Coming Soon: DECK - Full analog mastering signal chain emulator.
Currently in research phase, don't have a plan on the structure of the plugin yet, but it does
involve tape modelling, and possibly tube modelling.

## Coming Soon: \<unnamed resonator\> - Extend Karplus-Strong resonator
***Commissioned by Maldecoucou*** - ***Planning stage***

Turn any sound into pads, with three parallel resonators, tunable into a chord.
Each resonator has separate level and tuning controls, whereas the other parameters
are controlled by master controls.

The extended karplus-strong resonator is used extensively in Mutable Instruments Eurorack
modules, like Rings, Elements and Plaits. It can sound anywhere from a plucked string, to
woodwinds, to bells. Additionally, in the feedback path of the resonator, I'm adding a
diffuser, to make the harmonics more blurred and reverby.

## Coming Soon: \<untitled side exciter\>
***Requested by Bjarke and myself***
  
## Coming Soon: SHITPRESSOR \ BUFFER_MAXIMIZER (havent decided yet) - naïve so bad it's good compressor
Imagine you had half an hour to program a compressor, so intead of implementing it the traditional
way, you do it in the most naïve possible way, taking every possible shortcut. This is what
SHITPRESSOR \ BUFFER_MAXIMIZER does. It has three controls:
- Buffer size: controls the size of an internal buffer, similar to the sustain control on some more
  advanced compressors, like Image Line's Maximus, except shit.
- Target: the level that the compressor tries to push the sound towards, not exactly like threshold
  on a traditional compressor, but close.
- Depth: how hard the sound is compressed

The way it works is remarcably simple:
- The input is fed into a buffer of variable length.
- The peak loudness of the buffer is calculated at every step.
- The volume of the output is scaled so that the buffer peaks at the selected target.
- Depth is a percentage from 0 to 200%, at 100% percent, the buffer peaks at the target
  loudness, less than that and the compressor only takes it partway there, more than that
  and the compressor overshoots, making it shit.
  
You might have noticed the absence of an attack and release control, this is because this
compressor is terrible, and will introduce a lot of annoying clicks and pops to your sound
and generally distort the hell out of it. Enjoy.


# Suggestions and Ideas Backlog

These may never see the light of day. For plugins being actively worked on, see the list above instead.
- GROOVER: tempo-synced delay network. Has six delay times: 1, 2, 3, 5, 7, 11 steps. Each delay time
  is used on a separate delay line. The six delay lines can be in parallel or in series, the parallel
  or series connection can be varied continuously, so that with in-between values, the delay network
  can be quite complex. There is feedback control, which is six separate feedback paths for each
  delay when in parallel, and one global feedback for the entire chain when in series. The time can be
  multiplied or divided by integer amounts with a macro control.
- \<untitled beat-repeat thing\>: makes your boring beat less boring. Suggested by Bjarke. 
- STARVE: emulation of tube distortion with power-starvation dynamics artifacts.
- PENDULUM: pendulum distortion =)
- FFT_SHIMMER: uses the FFT engine for diffusion (blurring) and for pitch shifting,
has an added delay network in the feedback path, as well as a traditional time-domain
vibrato-like effect for a more chorus-y sound.
- FFT_DYNAMO: uses the FFT engine for spectral dynamic effects. Has these features:
    - Spectral compander: pushes all bin loudnesses towards a constant value, so
    the ideal output has the same energy per frequency as pink noise at -6dB peak.
    At negative levels of compander, bins are pushed away from the ideal -6dB.
    - Attack and release for all gain changes applied to bins.
- FFT_SMEAR: various methods of smearing bins with nearby bins. This is implemented
with a variety of filters:
    - Box average
    - Gaussian average
    - Median of amplitudes
    - Min of amplitdes
    - Max of amplitudes
    - Sharpen
- FFT_PHASER: a phaser implemented with FFT. Each bin has an associated phasor
which modulates the phase. The phasors can be offset from each other in phase and 
frequency, creating various interesting effects. Each bin has also
an associated sine wave oscillator, which modulates the amplitude, again phase,
amplitude and frequency of the oscillator can be changed.
- FFT_FUCK: a collection of weird glitchy spectral effects, beyond what SpecOps
can do, including a more in-depth take on the "mp3-ify" effect, which applies
bin-wise bit reduction. Effects where FFT and iFFT sizes don't match and the input
is mapped in various interesting ways to fit the size of the iFFT. A bin-wise
saturation effect, bin clustering in various ways (similar bins are combined),
bin sorting or partial sorting (a halted merge sort or quick-sort on bins by
amplitude), imaginary-real swapping. Various ways of permutating bins. Various
ways to smear bins (averaging with neighbors) or other convolutions borrowed from
the image processing world. Speaking of image processing:
- WAV_TO_PNG: a stand-alone application that converts a wave file into a png.
It collapses the 4-dimensions of the FFT (left_phase, right_phase, left_amplitude,
right_amplitude) into three dimensions (mid_phase, mid_amp, amp_panning) and then
turns each bin into a pixel, where the three dimensions are represented by RGB
values. The full wave file is thus converted into a matrix of pixels, and is
stored as a PNG, it also allows the reverse to happen. This can be used to
experiment with image filters on audio as well as using convolutional neural
networks for audio processing.
Specifically the conversion happens as follows:
    - mid_amp: lightness
    - pan: red-green balance
    - phase: yellow-blue balance
  
# Dependency Tree For Code Reuse (dot)
```dot
digraph G {
    rankdir=TD
    fontname="sans"
    node [color="black",style="filled",shape="box",fillcolor="white",fontname="sans"];
    splines=false
    edge [arrowhead="none", color="#00000060"]
    ranksep=1.25

    subgraph cluster{
        rank=same
        subgraph cluster_mod{
            label = "Circuit Modelling Plugins";
            style=filled;
            color=lightgrey;
            deck [label="DECK\ntape deck"];
            flick [label="FLICKER\ntube preamp"];
            chan [label="CHANNEL\nmixer insert"];
            starve [label="STARVE\namp and cab"];
        };
        
        subgraph cluster_creat{
            label = "Creative Plugins"
            style=filled;
            color=lightgrey;
            vibe [label="VIBE_MACHINE\nvaporwave goodness"]
            quant [label="STOCHASTIC\nquantizer on steroids"]
            glitch [label="GLITCH_DIV\nglitchy pitch shifter"]
            buffer [label="BUFFER_FUCK\nbuffer mangling,\nchaotic self-modulation"];
        };
        
        subgraph cluster_phys{
            label = "Physical Modelling Plugins"
            style=filled;
            color=lightgrey;
            chaos[label="CHAOS_OSC\ndouble pendulum"]
            res[label="<unnamed>\nmodal resonator\nextended kar+strong"]
            artifact[label="ARTIFACT\nwow, flutter, scrape\ndropouts, chorus"]
        };
        
        subgraph cluster_fft{
            label = "Spectral Plugins"
            style=filled;
            color=lightgrey;
            freeze[label="FFT_FREEZE\nspectral freeze"]
        };
        
        subgraph cluster_synth{
            label = "Synth Voices"
            style=filled;
            color=lightgrey;
            mikro[label="MIKROSYN\nphase distortion synth"]
            grain[label="GRAINTABLE\ngranular wavetable\nMI Beads idle mode"]
        };
    }

    
      deck -> slew;
      deck -> hyst;
      deck -> trans;
      deck -> fet;
      deck -> gap;
      deck -> choke;
      deck -> coupler;
      deck -> eq;
      deck -> allpass;
      deck -> svf;
      deck -> noise_white;
     flick -> tube;
     flick -> trans;
     flick -> choke;
     flick -> coupler;
     flick -> slew;
     flick -> noise_white;
      chan -> fet;
      chan -> trans;
      chan -> eq;
      chan -> choke;
      chan -> coupler;
      chan -> noise_white;
    starve -> tube;
    starve -> trans;
    starve -> diode;
    starve -> eq;
    starve -> cone;
    starve -> choke;
    starve -> coupler;
    
    vibe -> delay_line;
    vibe -> diffuser;
    vibe -> hyst;
    vibe -> slew;
    vibe -> svf;
    vibe -> flutter;
    quant -> diff;
    quant -> integ;
    quant -> noise_white;
    glitch -> svf;
    glitch -> noise_white;
    buffer -> noise_white;
    buffer -> general_sat;
    buffer -> delay_line;
    
    chaos -> c_integ;
    chaos -> integ;
    chaos -> diff;
    chaos -> noise_white;
    chaos -> svf;
    chaos -> general_sat;
    res -> damp;
    res -> bank;
    res -> diffuser
    artifact -> flutter;
    artifact -> geiger;
    
    freeze -> noise_white;
    freeze -> fft_lib;
    
    grain -> wave;
    grain -> TBD;
    mikro -> basic_syn;
    mikro -> TBD;
    
    subgraph cluster1{
        subgraph cluster1_mod{
            label="Circuit Modelling Meta-plugins";
            style=filled;
            color=lightgrey;
            tube [label="TUBE\nsaturation"];
            fet [label="TRANSISTOR\nsaturation"];
            trans [label="TRANSFORMER\nsaturation/tone"];
            diode [label="DIODE\ndiode clipping"];
            eq [label="REAL_EQ\nanalog equalizer"];
            cone [label="CONE\nspeaker sim"];
            choke [label="CHOKE\nchoking inductor\nnon-linear 1-pole LP"];
            coupler [label="COUPLER\ncoupling capacitor\nnon-linear 1-pole HP"];
            gap [label="GAP\ntape head gap\nnon-linear comb filter"];
            
            eq -> rsvf;
            choke -> slew;
            trans -> slew;
            trans -> hyst;
            
            slew [label="SLEW_CLIP\nnon-linear filter"];
            hyst [label="HYSTERESIS\nmagnetic saturation"];
            rsvf [label="REAL_SVF\nnon-linear filter\nAW Capacitor2"];
        }
        
        subgraph cluster1_phys{
            label="Physical Modelling Meta-plugins";
            style=filled;
            color=lightgrey;
            diffuser [label="DIFFUSER\nroom reflections"];
            flutter [label="WOW_N_FLUTTER\ntape wow and flutter lfo"];
            damp [label="DAMPENED_STRING\nextended karplus strong"]
            bank [label="MODAL_BANK\nmodal resonator"]
        }
        
        subgraph cluster1_syn{
            label="Synthesis Meta-plugins";
            style=filled;
            color=lightgrey;
            basic_syn [label="BASIC_SYNTH\n circular integrator oscs"]
            wave [label="WAVETABLES\n circular integrator tables"]
        }
    }
    
       tube -> noise_pink;
       tube -> noise_white;
       tube -> general_sat;
       tube -> integ;
       tube -> diff;
        fet -> general_sat;
        fet -> integ;
        fet -> diff;
        fet -> noise_white;
      trans -> integ;
      trans -> diff;
      trans -> noise_white;
      diode -> general_sat;
      diode -> diff;
      diode -> integ;
      diode -> noise_white;
       cone -> TBD;
      choke -> diff;
      choke -> integ;
      choke -> noise_white;
    coupler -> diff;
    coupler -> general_sat;
    coupler -> integ;
    coupler -> noise_white;
        gap -> delay_line;
        gap -> TBD;
       slew -> diff;
       slew -> integ;
       slew -> general_sat;
       hyst -> diff;
       hyst -> integ;
       hyst -> general_sat;
       rsvf -> TBD;
       
    diffuser -> delay_line;
    flutter -> noise_white;
    flutter -> geiger;
    flutter -> svf;
    damp -> delay_line;
    damp -> TBD;
    bank -> svf;
       
    basic_syn -> eg;
    basic_syn -> svf;
    basic_syn -> c_integ;
    wave -> eg;
    wave -> svf;
    wave -> lut;
    wave -> c_integ;
    
    TBD [fontcolor=red, label="to be determined"]
    
    subgraph cluster2 {
        label="DSP Lab Library"
        style=filled;
        color=lightgrey;
        allpass;
        svf;
        general_sat [label="generalized\nsaturation"];
        integ [label="integrator\nvariable leak"];
        c_integ [label="circular\nintegrator"];
        diff [label="derivative"];
        noise_white;
        noise_pink;
        delay_line;
        geiger;
        fft_lib;
        eg;
        lut;
        
        resample [fontcolor=red,label=<<B>downsample/upsample<br/>used my almost everything     </B>>]
        
        lut -> interpolate;
        delay_line -> interpolate;
        resample -> interpolate;
    }
    
    slew -> resample [style=invis] // constraint
    interpolate -> TBD [style=invis] // constraint   
}```
