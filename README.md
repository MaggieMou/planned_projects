# Planned Projects
Here is a list of upcoming plugins and applications. If you want to add things, please make a new issue.

## List of Planned Projects
- VIBE_MACHINE: instant vaporwave-ifyer. Combination of a granular delay, pitch shifter,
distortion and chorus.
- STARVE: emulation of tube distortion with power-starvation dynamics artifacts.
- MIKROSYN: minimalistic subtractive synthesizer with some unusual features (tri-saw
core into sin shaper into tanh oscillator (can make all classic waveforms and more)
mix with noise, into pitch-follow bit crush into LPG).
- PENDULUM: pendulum distortion =)
- GRAINTABLE: somewhere between a wavetable synth and a granular synth. Grains are
synthesized by picking a place on the wavetable.
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
