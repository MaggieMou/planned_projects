# Planned Projects
Here is a list of upcoming plugins and applications. If you want to add things, please make a new issue.

## List of Planned Projects
- VIBE_MACHINE: instant vaporwave-ifyer. Combination of a granular delay, pitch shifter,
distortion and chorus.
- STARVE: emulation of tube distortion with power-starvation dynamics artifacts.
- MIKROSYN: minimalistic subtractive synthesizer with some unusual features (sine
osc with phasor distortion, pitch follow sample rate reducer, low-pass gate).
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
