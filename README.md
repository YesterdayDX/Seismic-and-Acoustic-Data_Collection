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
3. Open a terminal by pressing "***crtl+alt+t***", go to the work directory with command "***cd ~/collection***"
4. Run "***python3 sync_clock.py***" to sync the time of raspberry shake with the laptop. (Need the password of raspberry shake: shakeme)
5. Log in to raspberry shake with command "***ssh myshake@rs.local***", (password: shakeme) 

## Python Scripts and how to run them
### On Raspberryshake
The scripts are located under path ~/dataCollection/
- **data_collect.py** 
  - The script to do the data collection.
  - This a stable version, store the seismic and acoustic data locally
  - **How to run**: *python3 data_collect.py -f $FILENAME -c $CHANNEL* 
    -  *$FILENAME* is an essential argument refering to the name of the current round of experiment.
    -  *$CHANNEL* refers to # of microphones used in data collection. 
       -  $CHANNEL = 0 ---> Do not collect acoustic data
       -  $CHANNEL = 1 ---> Collect data from 1 microphone [Default value]
       -  $CHANNEL = 4 ---> Collect data from all 4 microphones
  - **Data location**: *~/dataCollection/data/$FILENAME/*
    -  Will generate 5 files: 
      -  AUD_$FILENAME.csv ---> acoustic data
      -  EHZ_$FILENAME.csv, ENE_$FILENAME.csv, ENN_$FILENAME.csv, ENZ_$FILENAME.csv ---> seismic data
  -  **How to stop**: press "ctrl+C"
  -  **Important:** Use this script to do long time data collection.

- **acoustic_server.py**
   - This is a helper function for real time acoustic data demonstration.
   - Will not store any data locally.

### On Laptop
The scripts are located under path "~/collection/"
- **realtime_show_seismic.py**
  - This script is for real time showing the seismic curves.
  - **How to run**: *python3 realtime_show_seismic -s $StationID*
    - $StationID -- Station IS of raspberry shake
  - **How to stop**: Press "ctr+C"
- **realtime_show_acoustic.py**
  - This script is for real time showing the acoustic curves.
  - **How to run**: *python3 realtime_show_seismic
  - **How to stop**: Press "ctr+C"
  - **Only work when "acoustic_server.py" is running on raspberry shake**

## Some notes
### All scripts (laptop & RaspberryShake) are run with "*python3*" instead of "*python*"
### Disconnect the laptop and leave the sensor alone
- Idea **tmux**
- **tmux** is a terminal multiplexer, it allows the scripts keep running after the ssh connection broken.
- **How to use**
   - Create a tmux session: *tmux new -s $SESSION_ID, (e.g., tmux new -s data_collect)*
   - Run your code
      - "*cd ~/dataCollection.*"
      - "*python3 data_collect.py -f test -c 4*"
   - Detached from tmux session: press ctrl+b, then press d
   - Now the script will keep running when the laptop is disconnected.
   - We can re-join the tmux session by "*tmux a -t $SESSION_ID*"
      - Use "*tmux ls*" to see activate tmux sessions
### Use Battery
- Can use battery to provide power for raspberry shake. But currently don't get a good battery which could provide stable power supply. Data may loss, program running speed may be slower, because electric current is not stable.
- Battery may not work under low temperature is low.
### Data Collection: time of duration
- Acoustic data is high volumn, speed of data generation may be higher than the speed of writing acoustic data to files. 
- I would suggest short time of duration (e.g., 10 mins) for each round.
- data_collection.py can run for hours while collecting 1 microphone acoustic data.
