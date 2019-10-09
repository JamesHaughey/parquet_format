# CSV vs Parquet formats for data storage

### TL:DR
Using the Parquet format built into the Pandas package on one 2gb file of mixed data types is faster than reading / writing to a CSV and produces smaller files by significant margins. The only downside is that the files cannot be read natively by Excel.
- Writing files is over twenty times faster
- Reading files is nearly four times faster
- File sizes are thirteen times smaller

### What is Parquet?
Parquet is an open source standard for storing columnar data, developed by Twitter & Cloudera it is now maintained by the Apache software foundation. It is suported in both Python & R programming languages and by many SQL engines and distributed processing frameworks like Hadoop / Spark. 
It employs a variety of strategies to store data efficiently but works most efficiently on numeric data. See [Parquet Methodology Presentation](FIXME INSERT LINK HERE) for more details.

### Testing Methodology
I have used a single large file stored in memory in Python - this file contains a mix of numeric, string and datetime formatted data which should be fairly representative of an average dataset for analysis.
I am saving this file as both a CSV and parquet file, with and without compression and then repeating this test five times.
We are measuring the time to write the file, the size it takes up on the drive and then how long it takes to read that file back into memory.
This is being done on Windows 10 on a SSD drive.

### Results

