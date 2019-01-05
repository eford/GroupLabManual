+++
title = "CyberLAMP"
date = "8 Jan 2019"
type = "page"
hidden = false
weight = 500

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

## [CyberLAMP Wiki](https://wikispaces.psu.edu/display/CyberLAMP/CyberLAMP+Documentation+and+User+Manualhttps://wikispaces.psu.edu/display/CyberLAMP/CyberLAMP+Documentation+and+User+Manual)

You can submit a job to the CyberLAMP cluster's CPU nodes (if you're interested, there are several other options to make use of GPUs or Intel Phis) by using 
```
qsub -A cyberlamp script.pbs
```
or replacing the "-A" line in the pbs script with 
```
#PBS -A cyberlamp
```

For CyberLAMP only, there are several options that you can specify by adding an "-l" flag, either on the command line or in the pbs script
```
#PBS -l qos=cl_debug  # Debug job, should start quickly, must finish within 1 hour, max of 2 jobs per user
#PBS -l qos=cl_open   # Low-priority jobs, can run as many as you like, max wall clock time of 192 hours, must be preemptible)
#PBS -l qos=cl_himem  # High memory job, 1GB of memory per node
#PBS -l qos=cl_gpu    # Single-GPU job 
#PBS -l qos=cl_higpu  # Multi-GPU jobs (up to 4)
#PBS -l qos=cl_phi    # Phi job
```
If you don't specify any of these, it will be a "standard" CyberLAMP job (max wall clock time of 362 hours)

See the [CyberLAMP Wiki](https://wikispaces.psu.edu/display/CyberLAMP/CyberLAMP+Documentation+and+User+Manualhttps://wikispaces.psu.edu/display/CyberLAMP/CyberLAMP+Documentation+and+User+Manual) for updates to queue policies and additional info.


