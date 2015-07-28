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

Molasses is a **Module Oriented Large Archive Specialized Slow Exhaustive
Seacher**. Lame initialism aside, it is esentially Shazam or Midomi for music
modules instead of sampled audio formats such as 'mp3' and 'wav.' That is,
Molasses takes in a sampled audio file in 'wav' format and finds the closest
matching module. Molasses is slower\* than these
online services but has the advantages of being almost completely exhaustive for
tracker music. 

The motivation behind Molasses has a backstory that is too long to put near the
top of this page, but is available for the extremely bored reader here.

Brief Technical Overview
------------------------
Under the hood, it uses the fingerprint-based matching algorithm implemented in
the https://github.com/worldveil/dejavu project by Will Drevo, though it does
not rely on a mysql backend. Soundconverter (gstreamer-based) is used to convert
modules to wav format so that they can be fingerprinted. 

The reasoning behind the lack of a mysql database despite the intent of the
dejavu project is simple.  Even when only considering the 2007 snapshot of the
http://www.modarchive.org, there are around 120,000 modules to search through.
The required database would be immense by personal computing standards--dejavu's
documentation states that ~377MB is needed to store fingerprints for 45 tracks.
Even if we make the preposterous assumption that the average module is 1/2 the
duration of a mainstream pop music track, that comes out to ~500GB for the
database.

Therefore, each time a search is performed, Molasses essentially performs the
"indexing" stage of dejavu by processing each module in the archive. Processing
is very straightforward: each module is converted to wav format, fingerprinted,
and match/aligned with the input sample.

Performance
-----------
Despite being implemented in Python 2.7 and mostly unoptimized, Molasses is
capable of fingerprinting around 1 module (limited to 30s duration) every 3
seconds on an i5-2520M (~3GHz 2C/4T Sandy Bridge). This time includes the entire
conversion process, FFTs, and so on, meaning that modarchive in its entirety can
be searched in a matter of days. 

Molasses can take advantage of multi-core CPUs (via Python's multiprocessing
module), and if you're confident that the sample you're using to search starts
near the beginning of the targeted module, you can adjust the duration that each
module is fingerprinted. Processing time is roughly linear to fingerprinting
duration so limiting the duration to 15s should cut processing time in about
half.
