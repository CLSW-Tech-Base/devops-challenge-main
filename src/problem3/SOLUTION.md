Provide your solution here:
1. connect to vm and check if the VM in fact having 99% storage usages. (could be tools faulty)
2. identify the directory that causing the high storage usages. 
3. check for the directory that causing the high storage usages and identify the files 
   1. whether any files should be remove by the service but failed to
   2. whether the files is intended to be created (ie log file) and the file grow bigger as time

Case 1: if the file should be remove but failed, then should identify the root cause. 
- whether is using by service that caused deletion fail
- or the nginx service does not clean up at all

Case 2: if the files (log file) is intended to be created but file size grow as time
- could be nginx write everything into the log file, as such, should adjust the log level (not putting everything into file)
- if the file grow as expected, migrate the data to somewhere else (if want to keep it), then truncate the file (basically clean up the content so the service can continue write)

Preventions:
Case 1: lower down the alert, instead of 99% (which is super critical) set to 75% so that can execute proactive data cleanup (before causing service down as 99% most likely unable to maintain the service availablity)

Case 2: ship the log file to external location from time to time (or when the alert triggered), to keep the local log file minimal

[go back to main](/README.md)