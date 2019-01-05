+++
title = "Storage at ACI"
date = "8 Jan 2019"
type = "page"
hidden = false
weight = 300
+++

You can store data in the following locations:

   - Your home directory (least space, least fast, fully backed up, batch jobs should write to here or read large inputs from your home directory): `cd ~`
   - Our group directory (significant space, fast, regularly backed up): `cd /storage/group/ebf11/default`
   If you're storing data that you're not trying to share with others in our group, then please create a subdirectory with your username for your files.
   If you're storing data that you're trying to share with others in our group (e.g., software, data files that multiple people will be reading), then please create a directory with a name that others will be able to recognize easily.  
   For example, since julia development is often faster than ACI updates pacakges, I've been installing julia into our group directory.  E.g. /storage/group/ebf11/default/julia/bin/julia is a symlink to a recent (but not necessarily the most recent) version.  
   Note that the Jupyter notebook server currently doesn't have access to our group directory.  
  - Your work space (fast, regularly backed up): /storage/work/userid
  - scratch space (very fast, not backedup up, may be automatically deleted to make room for other people after some number of days):  /gpfs/scratch/userid


