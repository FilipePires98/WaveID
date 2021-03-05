# WaveID
A Music Identifier based on Vector Quantization and Applied Clustering

## Description

The programs implemented in C++ have the purpose of analysing and encoding audio files and ultimately being capable of, from a small audio segment, identifying the music that it most likely belongs to.

Along with the description of the solution, we also discuss the effects of the variation of the programs’ parameters and how accurate are the results. 

## Repository Structure

/codebook    - codebook examples

/report      - written report explaining our design choices, presenting results from parameter variation and conclusions of those results

/sampleTests - audio segments already pre-processed and ready to be used as query songs

/wavFiles    - audio dataset of song clips, in stereo

## Data Visualization

<p float="left">
  <img src="https://github.com/FilipePires98/WaveID/blob/master/report/sample01_stereo_1.png" width="360px">
  <img src="https://github.com/FilipePires98/WaveID/blob/master/report/sample01_16_1.png" width="360px">
</p>

Histograms before and after conversion to mono.

<img src="https://github.com/FilipePires98/WaveID/blob/master/report/stanford_quantization_wide.png" width="720px">

Example of a quantized waveform.

<img src="https://github.com/FilipePires98/WaveID/blob/master/report/pointsEx.png" width="540px">

Example of a 3-D visualization of point clusters

## Main Programs

 - **wavhist:** generates a histogram of a channel from the signal provided, possibly being the channel 0 or 1 if the signal is stereo or 0 if the signal is mono

 - **wavcmp:** given two songs, it's able to calculate the distance/error between them

 - **wavquant:** converts a stereo signal into a mono one, quantizes and reduces the sampling size if necessary

 - **wavcb:** from a mono file, generates the representing codebook

 - **wavfind:** given a query music segment, it's predicted the music to which it belongs

## Instructions to Build and Run 

  Build:   `$ make`

- **Visualize the frequency signature of the sample01 in mono:**

  Run:     `$ ./build/wavhist wavMonoFiles/sample01.wav 0`

- **Compare sample01 with sample04:**

  Run:     `$ ./build/wavcmp wavMonoFiles/sample01.wav wavMonoFiles/sample04.wav`

- **Quantize sample01 with 8 bits and a reduction sampling rate factor of 4:**

  Run:     `$ ./build/wavquant -q 8 -r 4 wavFiles/sample01.wav wavMonoFiles/sample01.wav`

- **Generate the codebook for sample01 with block size of 800 samples, overlap factor of 20% and error threshold of 1%:**

  Run:     `$ ./build/wavcb wavMonoFiles/sample01.wav 800 0.2 0.01 2 codebook/sample01`

- **Generate the same codebook as the last example, but with parallelism(2 external threads and 2 internal threads):**

  Run:     `$ ./build/wavcb wavMonoFiles/sample01.wav 800 0.2 0.01 2 codebook/sample01 2 2`

- **Verify to which music does a a given music segment belong to:**

  Run:     `$ ./build/wavfind sampleTests/sampleTest.wav 200 0.1 codebook`
  
Majority of the scripts have mandatory arguments. To have information about them call them without parameters, like:

`$ ./build/<script_name>`

## Authors

The authors of this repository are André Pedrosa, Filipe Pires and João Alegria, and the project was developed for the Algorithmic Theory of Information Course of the Master's degree in Informatics Engineering of the University of Aveiro.

For further information, please read our [report](https://github.com/FilipePires98/WaveID/blob/master/report/report.pdf).
