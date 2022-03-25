https://drive.google.com/drive/folders/1PH_naUqXpnfSFrPPSY_nm4ZqYAo2OSti
# How to tune spark executor number, cores and executor memory?


~The following answer covers the 3 main aspects mentioned in title - number of executors, executor memory and number of cores.
There may be other parameters like driver memory and others which I did not address as of this answer, but would like to add in near future.~

## Case 1 Hardware - 6 Nodes, and Each node 16 cores, 64 GB RAM

Each executor is a JVM instance. So we can have multiple executors in a single Node

First 1 core and 1 GB is needed for OS and Hadoop Daemons, so available are 15 cores, 63 GB RAM for each node

- Start with how to choose number of cores:

   1. Number of cores = Concurrent tasks as executor can run 

   2. So we might think, more concurrent tasks for each executor will give better performance. But research shows that
   any application with more than 5 concurrent tasks, would lead to bad show. So stick this to 5.

   3. This number came from the ability of executor and not from how many cores a system has. So the number 5 stays same
   even if you have double(32) cores in the CPU.
