# AudioTransform

AudioTransform is a package for modifying mono audio files of any sample rate, for use in augmenting datasets of audio.

Operations:
* load/save audio data
* resample
* invert polarity
* scale amplitude
* apply gain adjustments in decibels
* normalize amplitude
* digitally clip amplitude
* pad with silence
* varispeed - adjust time/pitch by altering playback speed
* mix two audio files
* static low-pass filter
* dynamic low-pass filter
* static high-pass filter
* convolution reverb

# Installation

```
# make virtual environment with Python 3.7
conda create -n AudioTransform python=3.7
source activate AudioTransform

# clone repository
git clone git@github.com:speechLabBcCuny/AudioTransform.git
cd AudioTransform

# install requirements from pip
pip install -r requirements.txt

# set up jupyter kernel
conda install ipykernel
ipython kernel install --user --name=AudioTransform     

# start Jupyter server
jupyter notebook --no-browser --port=8889

# on local machine
ssh -N -f -L localhost:8888:localhost:8889 [user]@[server]
```

# How To

See `AugmentAudio.ipynb` for examples of how to process audio.

Note - transformations are applied to the object itself, allowing method chaining for complex signal chains.

If a transformation is only being applied temporarily (e.g. scaling amplitude during mixing),
use the copy() method to create a new audio file to transform.

Example:

```
audio1 = AudioFile('example1.wav')
audio2 = AudioFile('example2.wav')

# audio1 is mixed with (audio2 * 0.5) - after this operation, audio2 is now scaled by 0.5
audio1.mix(audio2.scale(0.5), relative_start=0.0)

# The following line will mix audio1 with (audio2 * 0.5) - audio2 remains unchanged by this operation
audio1.mix(audio2.copy().scale(0.5), relative_start=0.0)
```

# Run Recipes

```
python3 <recipe_name>.py -i <input_dir> -o <output_dir>
```