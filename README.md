PPCAS v.1
=========
Probabilistic Pairwise model for Consistency-based multiple alignment in Apache Spark (PPCAS), able to generate the probabilistic pairwise model for large datasets of proteins and able to store it in the T-Coffee format.

Prerequisites
--------------
PPCAS compilation requires the following tools installed on your system ``make`` and ``gcc-c++``.

The execution requires a ``Hadoop`` and ``Spark`` infraestructure with the environment variables correctly set and its ``path``. Also a ``Python`` installation with ``Numpy`` is needed.


Compile 
--------
Download the git repository on your computer.
    
Make sure you have installed the required dependencies listed above. 
When done, move in the project root folder and enter the following commands:     
    
    $ make
    

The shared library will be automatically generated.


Usage
--------
It is included a script named ``run`` which executes PPCAS with the required and optional parameters.

Required parameters:

    $ -i [sequence_file]
    $ -m [master_spark_ip]
    
Optional parameters:

    $ -h (hdfs path, default: /user/root)
    $ -o (output, collection of files)
    $ -p (number of partitions, default: number of sequences)
    $ -t (T-Coffee output, single file)
    

Example
--------

There are input sequences in the examples folder.

``BB11001.tfa`` a small dataset from ``BAliBASE``.

``ghf13_*`` being  ``*`` the number of sequences obtained from ``HomFam`` dataset.

Calculate the library with 4 partitions (BB11001.tfa containts 4 sequences):

    $ ./run.sh -i BB11001.tfa -m 192.168.101.51
    
Calculate the library with 6 partitions (Faster if the infraestrucutre containts 6 cores or more):  
    
    $ ./run.sh -i BB11001.tfa -m 192.168.101.51 -p 6
    
Calculate the library with 4 partitions and store the result in T-Coffee format. It uses the hdfs://user/user_name to collect the temporary data:
    
    $ ./run.sh -i BB11001.tfa -m 192.168.101.51 -t - h /user/user_name
