## GSLib -- The Granular Synthesis Library 

The GSLib library implements asynchronous granular synthesis, with flexible control
over the timbre, pitch, time and spatialization of the resulting grain stream. It is freely distributable under the MIT license (see below). 


### COMPILING 
To use in a project, include grain_engine.c, grain_source.c and pdf.c in your project.  See ["example/annotated-granular.c"](example/annotated-granular.c) for an example implementation (written for use for the ancient [Allegro](http://www.talula.demon.co.uk/allegro)  but easily adaptable for other libraries).

### Operation
The library renders audio in buffers, of a certain specified length. These buffers are
filled with the grains from the synthesis process, with the appropriate transformations.
Specification of the audio is given via PDF’s for the parameter distributions. These
parameters are:


* Source: Discrete distribution over wave form sources that have been registered
with the library.
* Time: Continuous distribution over samples inside the source wave form.
* Pitch: Continuous distribution over pitches of grains.
* Pan: Continuous distribution over stereo pan position of grains.

#### Other parameters
The system also has a global grain density, grain length, maximum number of grains,
and parameters for adjusting the grain envelope. These are fixed and are not defined by
distributions. These parameters can be split into two groups: initialize time and run-time parameters.
Initialize time parameters must be set before synthesis begins, and cannot be modified

during synthesis. Run-time parameters are updated by callbacks which are called every
time the (sub)buffer is filled; these specify the time-varying properties of the synthesis.

## INITIALIZE TIME PARAMETERS 
At initialize time, the following parameters must be set:

*  Grain length. Length of grains in samples.
* Envelope type. GSLib supports two envelope types: Gaussian and linear. 
For the Gaussian type, the width of the kernel can be set; for the
linear type the attack/decay time as proportions of the grain length are given.
* Maximum number of grains. This fixs the maximum simulatenous number of
grains.
* Sample format

These parameters are initialize time to provide significant optimizations to the granulation
process, especially envelope precalculation.

## RUN TIME PARAMETERS 
The density of the grains (as a probability of activation at a time step) can be specified
at run time, as can all of the basic parameters described in Section A.1. For discrete distributions,
the parameters are specified as individual probabilities. For the continuous
parameters, Gaussian, half-Gaussian ( f (x) > 0 = 0 or f (x) < 0 = 0) and delta functions
can be used, as well as mixtures of these.

## LICENSE <
Copyright (c) 2006 John Williamson <br><br>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:<br><br>

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.<br><br>

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.<br><br>

