+++
title = "Eric's Old Getting Started Email"
date = "8 Jan 2019"
type = "page"
hidden = false
weight = 9999

[revealOptions]
transition= 'slide' # 'none','fade','concave','convex','zoom'
controls= true
progress= true
history= false
center= true
loop= false
pdfSeparateFragments= false
showNotes= true
+++

## How to use the new ACI-b cluster:

1. Make sure you have a PSU account

2. Request an ICS-ACI account with ebf11 as your sponsor (and wait until you receive a message that it's approved before proceeding to step #4)

3. Make sure you have setup "2 Factor Authentication" at https://2fa.psu.edu

### For interactive use 

4. Setup known hosts for aci-i:
  - download the script at http://iask.aci.ics.psu.edu/helpdesk/WebObjects/Helpdesk.woa/wa/CommonActions/download?dl=_v-GyIHWzyJMb3faYS9rQg&id=1
  - cd to the download location of roundRobinKnownHosts.sh
  - Make the script executable: chmod u+x roundRobinKnownHosts.sh
  - Run the script using the syntax: 
```
./roundRobinKnownHosts.sh aci-i.aci.ics.psu.edu >> ~/.ssh/known_hosts
```

5.  Log in to interactive node with either:
  - ssh -X aci-i.aci.ics.psu.edu
  - the Exceed OnDemand client (i.e., like a virtual desktop, more efficient than X11) see https://ics.psu.edu/computing-services/ics-aci-user-guide/#05-04-connecting-aci (Exceed OnDemand should soon be replaced by the ACI portal, see below)
  - the [ACI Portal](http://portal.aci.ics.psu.edu/)

6.  Check out what software packages are available
`module avail` or for more info `module spyder`

7.  Load any modules you will need for this session, e.g.
```
module load r             # this will load the default version, whatever that is
```
or 
```
module load python/2.7.8  # this specifies that you want a specific version of python
```
Note that you cannot load modules compiled with Intel and GCC at the same time; it has to be one or the other. 

8.  You can store data in the following locations:
   - Your home directory (least space, least fast, fully backed up, batch jobs should write to here or read large inputs from your home directory): cd ~
   - Our group directory (significant space, fast, regularly backed up): cd /gpfs/group/ebf11/default
   If you're storing data that you're not trying to share with others in our group, then please create a subdirectory with your username for your files.
   If you're storing data that you're trying to share with others in our group (e.g., software, data files that multiple people will be reading), then please create a directory with a name that others will be able to recognize easily.  
   For example, since julia development is often faster than ACI updates pacakges, I've been installing julia into our group directory.  E.g. /gpfs/group/ebf11/default/julia/bin/julia is a symlink to a recent (but not necessarily the most recent) version.  
  -  Your work space (fast, regularly backed up): /storage/work/userid
  - scratch space (very fast, not backedup up, may be automatically deleted to make room for other people after some number of days):  /gpfs/scratch/userid

9.  Compile codes, edit parameter files, do some modest computations that benefit from interactive access.  

### For batch use 

5.  Log in to the head node for batch jobs:
`ssh -X aci-b.aci.ics.psu.edu`

6.  Load any modules you will need for this session, e.g.
```
module load r             # this will load the default version, whatever that is
```
or 
```
module load python/2.7.8  # this specifies that you want a specific version of python
```
Note that you cannot load modules compiled with Intel and GCC at the same time; it has to be one or the other.  

7.  Change into directory you will run your job from, e.g. if you're using a directory named test in your work or scratch space, then 
```
cd /storage/work/userid
mkdir test
cd test
```
OR
```
ls /gpfs/scratch/userid  
mkdir test
cd test
```

{{% alert theme="warning" %}} _Warning:_ Files on the /gpfs/scratch file system are subject to automatic deletion after 30 days!  Use scratch for temporary files (e.g., created during jobs for short-term storage of large files), but NOT anything that you don't want to lose after the job finishes.
{{% /alert %}}

8.  Make a symlink or copy any codes and input data files your job will need into that directory.

9.  Create a PBS script to run your job (See URL for tutorial on PBS parameters, scripts and  examples.  Remember you'll need to include "module load ..." for any modules needed inside your PBS scripts. )
Your PBS script should include lines like the following to 
#!/bin/tcsh                   # Specifies which interpreter will be used for this script
#PBS -l walltime=24:00:00     # Maximum time your job is allowed to run  HH:MM:SS
#PBS -l nodes=1:ppn=1         # Specifies that your job needs one core on one node
#PBS -l pmem=512mb            # Specifies that your jobs needs 512 MB of real RAM and not just 
#PBS -l vmem=512mb            # Specifies that your jobs needs 512 MB of RAM
#PBS -A ebf11_a_g_sc_default  # Specifies to charge the job to our group's allocation
#PBS -j oe                    # Combines STDOUT and STDERR into a single file
#PBS -M userid@psu.edu        # Asks system to send userid an email when the job status changes
#module purge                 # If uncommented, clears out any modules loaded by default
#module load git              # If uncommented, would load the module git, etc.
cd $PBS_O_WORKDIR             # Changes to the directory that you were in when you submitted the job
[...follow with a standard shell script to actually do something...]

10.  Submit a PBS job:
a) Submit to the "Great" (aka "investor") queue to be charged to the Ford group allocation:
qsub -A ebf11_a_g_sc_default script.pbs
or 
qsub pbs_script.pbs # where there is a line in the PBS script like:
#PBS -A ebf11_a_g_sc_default

FYI- Collectively, our group has an allocation of 272 cores.  That means that we can "average" using as many 272 cores.  The scheduler should calculate our "average" based on a rolling 90 day period.  If there are additional nodes avaliable, then we should be able to use bursts of up to 4x272 = 1088 cores.  Of course, if we use a big burst for a while, then we have to use less than 277 cores for long enough to bring down our average.  Last I checked, we weren't using all of our allocation.  So feel free to put it to good use.  If there comes a time where we're getting in each other's way, then we'll deal with it then.  

b)  Alternatively, you can submit a job to the CyberLAMP cluster's CPU nodes (if you're interested, there are several other options to make use of GPUs or Intel Phis) by using 
qsub -A cyberlamp script.pbs
or replacing the "-A" line in the pbs script with 
#PBS -A cyberlamp
For CyberLAMP only, there are several options that you can specify by adding an "-l" flag, either on the command line or in the pbs script
#PBS -l qos=cl_debug  # Debug job, should start quickly, must finish within 1 hour, max of 2 jobs per user
#PBS -l qos=cl_open   # Low-priority jobs, can run as many as you like, max wall clock time of 96 hours, must be preemptible)
#PBS -l qos=cl_himem  # High memory job, 1GB of memory per node
#PBS -l qos=cl_gpu    # Single-GPU job 
#PBS -l qos=cl_higpu  # Multi-GPU jobs (up to 4)
#PBS -l qos=cl_phi    # Phi job
If you don't specify any of these, it will be a "standard" CyberLAMP job (max wall clock time of 169 hours)

c) Alternatively, you can submit a job to the "Open" allocation (more limited capabilities, but an option if you don't want to use our allocation) by specifying 
#PBS -A open

The open queue recently had limits of something like 100 or 200 cores per user, 20 cores per job and something like 24 or 48 hours wall clock time per job.  If/when the open queue is being heavily used, then jobs are likely to take longer to start if sent to the open queue, than if they had been sent to the "Great" queue (for "investors").  If we've used up our allocation or if you just have a bunch of low priority jobs that you want to run in the background, but don't want to get in the way of other research in our group, then it might make sense to use the open queue.  

d) If you want to know when your job might start, you can use the showstart command (e.g.,
showstart -e all 1@1:00:00
would predict which queue would be best for a job requesting 1 core for one hour.

11. Check on status of jobs w/ qstat and perform any job maintance w/ qdel, qhold, qrls... 

12.  For help (e.g., trouble shooting, installing software packages, etc.), send email to the ICS i-ASK Center <iask@ics.psu.edu> https://ics.psu.edu/computing-services/support/

WARNING:  At least for now, there is nothing to prevent any one of us from spending 3 months of computer time in just ~3 weeks.  So please: 
1) be careful to make sure you don't accidentally submit way more jobs than you intended (e.g., runaway script that submits jobs)

2) be careful to set appropriate wall clock limits in your PBS files that prevent your jobs from running way longer than you need (e.g., infinite loop, bug in an input file, scratching disk rather than computing, etc.), 

3) let the others of us know, if you plan to use more than ~140 cores solid for more than a week, so we can make sure your jobs won't get in someone else's way and/or come to a reasonable plan for sharing the allocation, 
 
4) email each other and cc me if you need someone to place a hold on their jobs so that your jobs to the investor queue can start, and 

5) let me know if someone/something is preventing you from getting your work done.


======== Example PBS Script ============
{{% panel %}}
```
#!/bin/tcsh
#PBS -A open              # Specifies job should use our allocation
#PBS -l nodes=1:ppn=1     # requests your job to be allocated 1 processor core
##PBS -l nodes=4          # if uncommented, this would requests 4 processor cores which may be spread across multiple nodes (or might be on the same node)
##PBS -l nodes=1:ppn=4    # if uncommented, this would requests 4 processor cores on a single node
#PBS -l walltime=24:00:00 # specifies a maximum run time in format of hh:mm:ss
#PBS -l pmem=1gb          # this requests 1GB of memory per process
#PBS -j oe                # combine the stdout and stderr into one file
#PBS -m abe               # tells PBS to send an email on abort, begin and/or exit
## *** TODO *** : modify the below line to have your email address ***
#PBS -M nobody@psu.edu    # send email to this address

#module purge             # If uncommented, clears out any modules loaded by default
#module load git          # If uncommented, would load the module git, etc.

cd $PBS_O_WORKDIR         # change into same directory as job was submitted from

# start julia and run julia commands in the subsequent filename (you'll need to copy/create that file in the directory you submit this job from)
/gpfs/group/ebf11/default/julia/bin/julia test.jl
```
{{% /panel %}}

For more information, see the ACI user guide at https://ics.psu.edu/computing-services/ics-aci-user-guide/, some of their online resources at https://ics.psu.edu/computing-services/ics-aci-training-resources/, or https://ics.psu.edu/computing-services/support/


