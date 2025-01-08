# hashcat-benchmarks
A centralized collection of full hashcat benchmarks done on the latest version with lots of GPUs. I would love to include GPU vendor information, but I don't think it's possible to retrieve it inside a docker container. You are welcome to contribute benchmarks from your own machines, just open a PR. Also, please stick to the same file naming scheme, and include machine specs if possible.  

I used the following bash snippet to run benchmarks on different machines from vast.ai:
```
wget https://hashcat.net/beta/hashcat-6.2.6%2B813.7z
apt install -y 7zip inxi
7zz x hashcat-6.2.6+813.7z
gpu_info=$(nvidia-smi --query-gpu=name,memory.total --format=csv,noheader | head -n1 | sed 's/, /,/g' | awk -F',' '{print $1 " " int($2/1024) "GB"}' | sed 's/ /_/g') && inxi -F > "/root/${gpu_info}.txt" && cd hashcat-6.2.6 && ./hashcat.bin -O -w 4 -b --benchmark-all | tee -a "/root/${gpu_info}.txt"
```

Note: some benchmarks were done on vast.ai's "unverified" instances, so performance may be lower than expected (I saw a 1060 run at 98C, yikes!), but that's mostly for old GPUs that there are few of available to rent, like the 10 series.

