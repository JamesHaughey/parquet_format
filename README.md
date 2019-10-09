# CSV vs Parquet formats for data storage

### TL:DR
Using the Parquet format built into the Pandas package on one 2gb file of mixed data types is faster than reading / writing to a CSV and produces smaller files by significant margins. The only downside is that the files cannot be read natively by Excel.
- Writing files is over twenty times faster
- Reading files is nearly four times faster
- File sizes are thirteen times smaller

### What is Parquet?
Parquet is an open source standard for storing columnar data, developed by Twitter & Cloudera it is now maintained by the Apache software foundation. It is suported in both Python & R programming languages and by many SQL engines and distributed processing frameworks like Hadoop / Spark. 
It employs a variety of strategies to store data efficiently but works most efficiently on numeric data. See [Parquet Methodology Presentation](https://youtu.be/MZNjmfx4LMc) for more details.

### Testing Methodology
I have used a single large file stored in memory in Python - this file contains a mix of numeric, string and datetime formatted data which should be fairly representative of an average dataset for analysis.

I am saving this file as both a CSV and parquet file, with and without compression and then repeating this test five times.

We are measuring the time to write the file, the size it takes up on the drive and then how long it takes to read that file back into memory.

This is being done on Windows 10 on a SSD drive.

See [Testing Notebook](https://github.com/JamesHaughey/parquet_format/blob/master/parquet_results.ipynb) for more details

### Results
<table id="T_f111dda2_ea6a_11e9_89a0_f894c23326a0" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >write_time</th>        <th class="col_heading level0 col1" >read_time</th>        <th class="col_heading level0 col2" >file_size</th>    </tr>    <tr>        <th class="index_name level0" >test</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>                <tr>                        <th id="T_f111dda2_ea6a_11e9_89a0_f894c23326a0level0_row0" class="row_heading level0 row0" >csv_compression</th>                        <td id="T_f111dda2_ea6a_11e9_89a0_f894c23326a0row0_col0" class="data row0 col0" >443.7s</td>                        <td id="T_f111dda2_ea6a_11e9_89a0_f894c23326a0row0_col1" class="data row0 col1" >44.0s</td>                        <td id="T_f111dda2_ea6a_11e9_89a0_f894c23326a0row0_col2" class="data row0 col2" >193mb</td>            </tr>            <tr>                        <th id="T_f111dda2_ea6a_11e9_89a0_f894c23326a0level0_row1" class="row_heading level0 row1" >csv_no_compression</th>                        <td id="T_f111dda2_ea6a_11e9_89a0_f894c23326a0row1_col0" class="data row1 col0" >345.9s</td>                        <td id="T_f111dda2_ea6a_11e9_89a0_f894c23326a0row1_col1" class="data row1 col1" >34.0s</td>                        <td id="T_f111dda2_ea6a_11e9_89a0_f894c23326a0row1_col2" class="data row1 col2" >2,435mb</td>            </tr>            <tr>                        <th id="T_f111dda2_ea6a_11e9_89a0_f894c23326a0level0_row2" class="row_heading level0 row2" >parquet_compression</th>                        <td id="T_f111dda2_ea6a_11e9_89a0_f894c23326a0row2_col0" class="data row2 col0" >16.0s</td>                        <td id="T_f111dda2_ea6a_11e9_89a0_f894c23326a0row2_col1" class="data row2 col1" >9.0s</td>                        <td id="T_f111dda2_ea6a_11e9_89a0_f894c23326a0row2_col2" class="data row2 col2" >182mb</td>            </tr>            <tr>                        <th id="T_f111dda2_ea6a_11e9_89a0_f894c23326a0level0_row3" class="row_heading level0 row3" >parquet_no_compression</th>                        <td id="T_f111dda2_ea6a_11e9_89a0_f894c23326a0row3_col0" class="data row3 col0" >15.8s</td>                        <td id="T_f111dda2_ea6a_11e9_89a0_f894c23326a0row3_col1" class="data row3 col1" >9.2s</td>                        <td id="T_f111dda2_ea6a_11e9_89a0_f894c23326a0row3_col2" class="data row3 col2" >182mb</td>            </tr>    </tbody></table>