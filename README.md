## Python Scripts and how to run them
### On Raspberryshake
The scripts are located under path "~/dataCollection/"
- *data_collect.py*
  - The script to do the data collection.
  - This a stable version, store the seismic and acoustic data locally
  - While running, only the curves of seismic data (not acoustic) can be shown in real-time by running "realtime_show_seismic.py" script in th laptop, see details bellow.
  - How to run: "./data_collect.py -f $filename"
    -  $filename is an essential argument
- *data_collect_with_socket.py*

### On Laptop
The scripts are located under path "~/collection/"
- realtime_show_acoustic.py
- realtime_show_seismic.py
