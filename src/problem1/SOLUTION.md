Provide your CLI command here:

```
# assume each transaction will be on single line
# assume the data is not fix case
grep -i "TSLA" transaction-log.txt | grep -i "sell" > ./output.txt
```