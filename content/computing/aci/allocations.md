+++
title = "ACI Allocations"
date = "8 Jan 2019"
type = "page"
hidden = false
weight = 300

theme = "psu" # "league"
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


There are several "allocations" that you can submit jobs against.  I'll list them starting with the ones that you should feel free to use very agressively and ending with two ways to submit jobs that are most likely to get in the way of another user.

### "The [ACI] open queue":   
```
#PBS -A open              
```
Pro:  Free to all PSU researchers.  
Con:  Most restrictions (e.g., 48 hours wall time limit).  Lowest priority to start.  Jobs can be suspended.  
More info: https://ics.psu.edu/computing-services/service-details/the-aci-b-open-queue/

### "CyberLAMP Open queue":
```
#PBS -A cyberlamp
#PBS -l qos=cl_open  
```
Pro:  Extra computer power for research groups in CyberLAMP team
Con:  Shared with other CyberLAMP users.  Lowest priority queue for CyberLAMP jobs to start.  Some extra limits (e.g., 96 hours wall time limit).  Jobs could be suspended.  
More info:  https://wikispaces.psu.edu/display/CyberLAMP/Queue+policies

### "Standard CyberLAMP queue":
```
#PBS -A cyberlamp
```
Pro:  Extra computer power for research groups in CyberLAMP team
Con:  Shared with other CyberLAMP users.  Some limites (e.g., 169 hour wall clock limit).  If you use a large fraction of a cluster for an extended period, then another CyberLAMP user might ask you to dial back usage.  
More info:  https://wikispaces.psu.edu/display/CyberLAMP/Queue+policies

### "Ford group allocation on ACI with no bursting" 
(also known as GReaT SLA=Guarenteed Responce Time Service Level Agreement)
```
#PBS -A  ebf11_a_g_sc_default 
#PBS -W x=FLAGS:ADVRES:ebf11_a_g_sc_default 
```
Pro:  Highest priority for jobs to start.  Jobs should be guarenteed to start within an hour, usually a few minutes, as long as our group as a whole doesn't already have 280 cores worth of jobs running and we haven't averaged using more than 280 cores over the past 90 days.  Won't risk using up our allocation in the future.
Con: If our group is already using 280 cores of jobs to be charged to this allocation, job will wait.
More info:  https://ics.psu.edu/computing-services/service-details/#GReaT (excluding reference to bursting)

### "Ford group allocation on ACI with bursting"
```
#PBS -A  ebf11_a_g_sc_default 
```
Pro:  Highest priority for jobs to start.  Jobs should be guarenteed to start within an hour, usually a few minutes, as long as our group as a whole doesn't already have 280 cores worth of jobs running and we haven't averaged using more than 280 cores over the past 90 days.  Even if 280 cores of jobs are already running, these get preference to start up to 1,120 cores worth of jobs (when above conditions met) relative to jobs submitted to 'The Open queue'.  
Con:  If our group uses over 280 cores at once for an extended period of time, then we would have to wait for the 90 day average to drop below 280 cores before we're elligible for jobs submitted to this allocation to allowed to start again
More info:  https://ics.psu.edu/computing-services/service-details/#GReaT

### "ICS co-hire High-Memory core queue"
```
#PBS -A  wff3_a_g_hc_default 
```
Pro:  If you need access to nodes with 1TB of RAM.
Con:  2 high-memory  nodes (each with 40 cores) shared among ~20 research groups.  Should be considerate of other users.
More info:  Undocumented.


