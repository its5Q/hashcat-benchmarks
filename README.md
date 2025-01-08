# hashcat-benchmarks
A centralized collection of full hashcat benchmarks done on the latest version with lots of GPUs. All contributions are welcome!  


The following bash snippet was used to run benchmarks on different machines from vast.ai:
```
wget https://hashcat.net/beta/hashcat-6.2.6%2B813.7z
apt install -y 7zip inxi
7zz x hashcat-6.2.6+813.7z
gpu_info=$(nvidia-smi --query-gpu=name,memory.total --format=csv,noheader | head -n1 | sed 's/, /,/g' | awk -F',' '{print $1 " " int($2/1024) "GB"}' | sed 's/ /_/g') && inxi -F > "/root/${gpu_info}.txt" && cd hashcat-6.2.6 && ./hashcat.bin -O -w 4 -b --benchmark-all | tee -a "/root/${gpu_info}.txt"
```


