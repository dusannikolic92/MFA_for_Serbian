# Tutorial
This is a tutorial on how to create automatic transcription for Serbian using the Montreal Forced Aligner. The tutorial is a shorter version of Dr. Chodroff's full tutorial (https://www.eleanorchodroff.com/tutorial/montreal-forced-aligner-v1-legacy.html). 
The tutorial covers the MacOS system, but in principle, it should work with Windows, too

## Installing MFA

First, install conda on your computer by following the instructions here: https://docs.conda.io/projects/conda/en/latest/user-guide/install/macos.html 
Next, open your terminal on MacOS by typing in 'terminal' (Windows 'cmd'). Type in the following codes: 

conda config --add channels conda-forge
conda install montreal-forced-aligner

## Downloading acoustic and textual dictionaries

Download acoustic and textual dictionaries of Croatian from the MFA database by running these two functions in the terminal.
```
mfa model download acoustic croatian_mfa
mfa model download dictionary croatian_mfa
```
Inspect these models to view a phone set using the mfa model inspect function.
```
mfa model inspect acoustic croatian_mfa
mfa model inspect dictionary croatian_mfa
```
## Prepare audio and TextGrids

Your task is to transcribe your recordings in Praat. The audio library I used is the Serbian dataset from CommonVoice (https://commonvoice.mozilla.org/en/datasets), which also includes transcriptions of the audio, that is, full sentences transcription. These sentences are not aligned in Praat and there are no TextGrids. 

To create TextGrids, either use (http://www.homepages.ucl.ac.uk/~uclyyix/ProsodyPro/) or follow my instructions in the video here: https://youtu.be/FBqvaQJr1ig. The audio also needs to be resampled to 16kHz, which you can do in Audacity.

## MFA Transcription

After I have created TextGrids, I placed both the TextGrid files and audio recordings into a single file, which I called "input", and I placed it on my Desktop. I also created "output" folder on Desktop. Be careful with directories. Make sure that you are using proper file and folder paths from this point on. 

First run the aligner

```
conda activate aligner
```

Then, start aligning by using the following pattern: mfa align corpus_directory dictionary acoustic_model output_directory. Because I transcribed 'test' and 'train' audio files, I have two separate codes. 

```
mfa align --clean /Users/dusan/Desktop/Train ~/Documents/MFA/pretrained_models/dictionary/croatian_mfa.dict  croatian_mfa /Users/dusan/Desktop/output/Train
mfa align --clean /Users/dusan/Desktop/Test ~/Documents/MFA/pretrained_models/dictionary/croatian_mfa.dict  croatian_mfa /Users/dusan/Desktop/output/Test
```

The aligned TextGrids are now in yout output folder!



