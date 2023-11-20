# Numerical sort
```bash
echo "2\n1\n4" | sort -n 
```

# Version sort
```bash
echo "2.04\n10.12.9.0\n4.48.0.1" | sort -V
```
Can be used to sort IP addresses.

# Field Separator
```bash
dig yahoo.com +short | sort -t . -n -k 1,1
```
We are sorting IP addresses this way.
Here, 
>`-t .`: Since IP addresses are separated by periods, you will tell the sort command to use a period/dot (.) as the field separator.
>
>`-k 1,1`: This option tells sort command field number to sort on. For instance, the -k 1,1 option sorts on the first field, which is the first octet of the IP address. We can add **multiple `-k`** options to **fine tune sorting**.

We can sort IP addresses by the last octet like this: 
```bash
sort -t . -n -k 4,4 filename
```
Maybe we want to sort by the first three octets. Then:
```bash
sort -t . -n -k 1,3 filename
```