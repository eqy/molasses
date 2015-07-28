Molasses
========

Module Oriented Large Archive Specialized Slow Exhaustive Seacher
-----------------------------------------------------------------

Usage:

    python molasses.py /path/to/target.[wav,mp3] /path/to/mod_archive /path/to/temp_directory [duration limit in seconds]

Duration limit is optional, use >= 30 if you are unsure if your target wav/mp3
starts at the beginning of the mod. Processing time is linear with duration
limit.

Dependencies:
+ dejavu (https://github.com/worldveil/dejavu has many other dependencies)
+ soundconverter
+ standard python modules (os,sys,subprocess,shutil,calendar,time,
    multiprocessing, pydub, collections)

Note that dejavu requires mysql and mysqldb, but you do not need to create or
initialize a database to use molasses.
