# ukbb_slicer
python based tool to extract specific fields(and all their instances) from UKBB csv file

1. We can use this tool in low memory mode, enabled by default, and one can run it on the landing space of SLURM systems. In low memory mode, working with mixed data types is not recommended.
2. Its easiest to use the salloc command to first a job allocated for you and then run the command
3. Many sample commands are provided in the run_ubb.sh script
4. We can pass the list of EIDs, and the program will extract field information only for those EIDs
5. If you want to extract all the rows in the input file, and you don't know the number of rows, enter a huge number, like 10 million, and the program will pick all the rows from the CSV file 
6. We can save the extracted fields in CSV or/and text format
7. Below is the usage for the utility

        usage: ukbiobank.py [-h] [-ef EIDSFILE | -n NUMROWS] [-v {0,1,2}] [-sc {0,1}] [-st {0,1}] [-l {0,1}]
                            csvfile fields

        positional arguments:
          csvfile               pass the path to the csv file containing the data from the ukbiobank
          fields                pass a comma separated values of all the fields you want to extract the information
                                about. please note that you need not to pass the instances ids, just path the root field
                                ids

        options:
          -h, --help            show this help message and exit
          -ef EIDSFILE, --eidsfile EIDSFILE
                                pass the path to the text file containing the list of eids. file should have only one eid
                                in one line without any header. please note that this approach is bit memory extensive as
                                we first load the csv file with all the rows, and selected columns, and then we apply the
                                filtering based on a list created from the eid passed by the user. Please try to pass
                                less number of columns, so that the program could run even on low memory system, On high
                                memory system there would not be any trouble
          -n NUMROWS, --numrows NUMROWS
                                pass the number of lines of data you want to see, in default mode we shall print 1000
                                rows
          -v {0,1,2}, --verbosity {0,1,2}
                                increase output verbosity, by default we only print the final dataframe as text, with
                                input as 2 we will also print the unique dict created, we will describe the stats of the
                                dataframe, etc...
          -sc {0,1}, --savecsv {0,1}
                                save the selected dataframe as a csv file
          -st {0,1}, --savetxt {0,1}
                                save the selected dataframe as a txt file
          -l {0,1}, --lowmemory {0,1}
                                enable or disable low memory mode, enabled by default
