# IntanToNWB
Convert Intan (rhd or rhs) files to NWB file format.

This program takes all data from an Intan file (.rhd or .rhs) and converts it to an .nwb file, an open-source data standard described by Neurodata Without Borders (NWB). NWB aims to encourage adoption of a unified data format to facilitate the sharing, archiving, use, and analysis of data by removing the barriers associated with data from different sources being stored in non-standard ways. More information on NWB can be found here: https://www.nwb.org/ . A large archive of neurophysiology data, DANDI (Distributed Archives for Neurophysiology Data Integration), is publicly available here: https://www.dandiarchive.org/ . This project hosts a vast number of datasets in the NWB format.

The converter is written in a Jupyter Notebook, using ipywidgets to create a user-friendly dashboard for configuring settings like filename, information about the recording session, and details of the conversion process, like file compression. However, the bulk of the program is written in Python, and if the Jupyter Notebook GUI is not desired, a call to the function 'convert_to_nwb' will allow for Python to complete the conversion without requiring Jupyter Notebook. Support for all file formats generated by Intan software is provided, including the traditional '.rhd' or '.rhs' files, as well as both the One File Per Signal and One File Per Channel formats. This program also supports merging of multiple .rhd/.rhs files, as long as they're consecutive, for combining multiple files of continuous data into a single .nwb file. The only data that can be generated by Intan software but not converted is Spike Data gathered from the real-time spike detection from the RHX software - this may be something we add to the converter in the future.

## Installation
To run this example, either download the 9 files:
1. IntanToNWB.ipynb
2. ConverterUI.py
3. ConvertIntanToNWB.py
4. ProcessData.py
5. ReadIntanData.py
6. ReadIntanHeader.py
7. ReadSettingsFile.py
8. SetupResources.py
9. WriteNWB.py

to the same directory and open them with Jupyter Notebook on your own machine (Jupyter must already be installed), or click the Binder link below to run it in a remote Docker container.

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/Intan-Technologies/IntanToNWB/HEAD)

This notebook depends on PyNWB, a Python NWB package that provides the HDF5 interface used for writing to NWB format. This notebook was written using version 2.0.0 of PyNWB.

## Usage
To read data from Intan files (.rhd or .rhs, or for other file formats, .dat), bring those files to the same directory this notebook is in, and change the "File to convert" to the file you wish to convert. After a period of time (progress can be monitored by reading the output print statements), an output file with the extension .nwb will be written in this directory.

If you wish to merge multiple continuous files into a single .NWB file, give the name of the earliest file in that recording session, and check "Merge Multiple Continuous Files" in the Advanced Settings section, and any files that continue from that recording session will automatically be merged.

If you wish to read non-traditional file formats (File Per Signal Type or File Per Channel), give the name of the Intan header file (by default, info.rhd or info.rhs) and ensure the corresponding .dat files are present in the same directory.

If you wish to automate conversion settings, alter the 'Example_NWB_Conversion_Settings.xlsx' file to the desired settings, and either run the UI with the 'Load conversion settings file' checkbox ticked, or run the convert_to_nwb() Python function directly with this .xlsx filename as an input argument.