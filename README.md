Molasses
========

Module Oriented Large Archive Specialized Slow Exhaustive Seacher
-----------------------------------------------------------------

Demo video:
https://www.youtube.com/watch?v=8MkqQ8N0UKA

Molasses's current greatest achievement is uncovering the source of the music in
this ancient Tom's Hardware video (https://www.youtube.com/watch?v=N1hg1zf7rrY)
as http://modarchive.org/index.php?request=view_by_moduleid&query=40309. 

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
