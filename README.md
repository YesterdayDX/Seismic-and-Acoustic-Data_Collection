# Seismic and Acoustic Data Collection
## Device setup
### Raspberry shake
- username: myshake
- password: shakeme
### Laptop
- username: Robot
- password:1qaz
### Connect the laptop with raspberry shake
1. Power on the raspberry shake.
2. Connect raspberry shake and the laptop with ethernet cable.
3. In laptop, open a browser, access "rs.local" (Need to wait several seconds for building the connection.
4. Remeber $IP (Ip address) and $StationID (Station ID) of the raspberry shake, the webpage will show that.
5. For example **$IP = 10.42.0.123** and **$StationID = R3596**.
6. Open a termianl on laptop, log in the raspberry shake with *ssh myshake@$IP*, (password: shakeme)  
   For example: ***ssh myshake@10.42.0.123***

## Python Scripts and how to run them
### On Raspberryshake
The scripts are located under path ~/dataCollection/
- **data_collect.py**
   --file_name $FILENAME 
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
  - **Script works when "data_collect.py" or "data_collect_with_socket.py" is running on raspberry shake**
- **realtime_show_acoustic.py**
  - This script is for real time showing the acoustic curves.
  - **How to run**: *python3 realtime_show_seismic --ip $IP*
    - $IP -- IP address of raspberry shake
  - **How to stop**: Press "ctr+C"
  - **Only work when "data_collect_with_socket.py" is running on raspberry shake**

## Some notes
### Disconnect the laptop and leave the sensor alone
- Idea **tmux**
- **tmux** is a terminal multiplexer, it allows the scripts keep running after the ssh connection broken.
### Use Battery
- Can use battery to provide power for raspberry shake. But currently don't get a good battery which could provide stable power supply. Data may loss, program running speed may be slower, because electric current is not stable.
### Data Collection: time of duration
- Acoustic data is high volumn, speed of data generation may be higher than the speed of writing acoustic data to files. 
- I would suggest short time of duration (e.g., 10 mins) for each round.
