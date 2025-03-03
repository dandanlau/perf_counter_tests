Goal:
Find out what counters or events are enabled in VMs. Customers often see counters reading 0 on a VM, either using uProf or linux perf. There are several possibilities:

1. KVM or Hypervisor blocked the access
2. Cloud vendor blocked access for security reasons.


These scripts and processes outlined will help identify the list of counters that might be blocked.

Prerequesites  
Install JQ: sudo apt-get install jq  
Install benchmark or applications that you want to run: stress-ng/coremark etc. Attached in the folder is a simple load/store memory access program  


Files in the zip:  
linux kernel 6.6 zen4 perf events json files.  
test.cpp - the load/store memory app  
extract_event_name_from_json.sh - it goes through the list of json and print out all the eventname into event_name.txt and event_name.csv  
extract_perf_stats.sh - take event_name.txt as input, runs "perf stat -e" command with each event name, and write counter result in perf_results.txt  


To update the .json for different kernels    
Download linux kernel source here: https://www.kernel.org/  
Extract json files from: /tools/perf/pmu-events/arch/x86/amdzen4/  


To collect the counters  
> extract_event_name_from_json.sh  

> extract_perf_stats.sh  

modify the app name in extract_perf_stats.sh as needed  

Generated files  
perf_results.txt - counter names with counter values  

perf_stat_zero_non_zero.txt - event names with zero/non-zero value for easy comparison between runs.  
