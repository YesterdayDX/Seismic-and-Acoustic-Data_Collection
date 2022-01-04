## Python Scripts and how to run them
### On Raspberryshake
The scripts are located under path ~/dataCollection/
- **data_collect.py**
  - The script to do the data collection.
  - This a stable version, store the seismic and acoustic data locally
  - While running, only the curves of seismic data (not acoustic) can be shown in real-time by running *realtime_show_seismic.py* script in th laptop, see details bellow.
  - **How to run**: <font color=Blue> *./data_collect.py -f $filename* <font>
    -  *$filename* is an essential argument refering to the name of the current round of experiment.
  - **Data location**: *~/dataCollection/data/$filename/*
    -  Will generate 5 files: 
      -  AUD_$filename.csv -- acoustic data
      -  EHZ_$filename.csv, ENE_$filename.csv, ENN_$filename.csv, ENZ_$filename.csv -- seismic data
  -  **How to stop**: press "ctrl+V"
- **data_collect_with_socket.py**

### On Laptop
The scripts are located under path "~/collection/"
- realtime_show_acoustic.py
- realtime_show_seismic.py

