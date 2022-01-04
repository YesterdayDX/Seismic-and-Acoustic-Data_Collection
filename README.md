## Python Scripts and how to run them
### On Raspberryshake
The scripts are located under path ~/dataCollection/
- **data_collect.py**
  - The script to do the data collection.
  - This a stable version, store the seismic and acoustic data locally
  - While running, only the curves of seismic data (not acoustic) can be shown in real-time by running *realtime_show_seismic.py* script in th laptop, see details bellow.
  - **How to run**: *python3 data_collect.py -f $filename* 
    -  *$filename* is an essential argument refering to the name of the current round of experiment.
  - **Data location**: *~/dataCollection/data/$filename/*
    -  Will generate 5 files: 
      -  AUD_$filename.csv -- acoustic data
      -  EHZ_$filename.csv, ENE_$filename.csv, ENN_$filename.csv, ENZ_$filename.csv -- seismic data
  -  **How to stop**: press "ctrl+C"
  -  **Important:** Use this script if we do not need to show acoustic curve in real-time.
- **data_collect_with_socket.py**
  - This script is an upgrade version of *data_collect.py*, curve of acoustic data can be shown in laptop, see bellow for details of showing data in real-time.
  - **How to run**: *python3 data_collect_with_socket.py -f $filename -s yes*
    - "-s yes" means the we create a socket to transmit acoustic data
  - **Important:** May exist bugs, use this script only for showing acoustic data in real-time

### On Laptop
The scripts are located under path "~/collection/"
- **realtime_show_seismic.py**
  - This script is for real time showing the seismic curves.
  - **How to run**: *python3 realtime_show_seismic --ip $IP --station $StationID*
    - $IP -- IP address of raspberry shake
    - $StationID -- Station IS of raspberry shake
  - **How to stop**: Press "ctr+C"
  - **Script works when "data_collect.py" or "data_collect_with_socket.py" is running on raspberry shake
- **realtime_show_acoustic.py**
  - This script is for real time showing the acoustic curves.
  - **How to run**: *python3 realtime_show_seismic --ip $IP*
    - $IP -- IP address of raspberry shake
  - **How to stop**: Press "ctr+C"
  - **Only work when "data_collect_with_socket.py" is running on raspberry shake

