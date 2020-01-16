+++
title = "Jupyter Notebook Server"
date = "8 Jan 2019"
type = "page"
hidden = false
weight = 200

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

### Instructions for Using Julia via the Jupyter Notebook server in the ICDS ACI Portal
1.  [Setup Julia kernel to work with ICDS-ACI](#setup-julia) (only needs to be done once per user)
2.  [Start a Jupyter Notebook session on ACI](#start-jupyter)
3.  [Clone your Github Repository on ACI](#clone-repo) (only need to do once per repository)

---

<a id="setup-julia"></a>
### Setup Julia kernel to work with ACI's Jupyter notebook server

- Browse to portal.aci.ics.psu.edu
- Login (if necessary)
- Click _Interactive Apps_ on top menu
- Before using Julia on ACI for the first time
   + Choose _ACI Interactive Desktop_
   + Click _Launch_
   + Wait while your job starts
   + Once the _Launch noVNC in new tab_ button appears, click it
- Open a terminal via second button on bottom toolbar
- Run the following code in the terminal

```shell
module load python/3.6.3-anaconda5.0.1
cd work
mkdir julia_depot
# Setup a Julia package depot in your ACI work directory
cd julia_depot
export JULIA_DEPOT_PATH=$PWD
echo "export JULIA_DEPOT_PATH=$PWD" >> ~/.bashrc
cd ..

# Install Julia in your work directory
mkdir julia_install
cd julia_install/
wget https://julialang-s3.julialang.org/bin/linux/x64/1.0/julia-1.0.2-linux-x86_64.tar.gz
tar -xf julia-1.0.2-linux-x86_64.tar.gz
cd julia-1.0.2

# Setup paths so Julia can be found
export PATH=$PWD/bin:$PATH
export LD_LIBRARY_PATH=$PWD/lib:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=$PWD/lib/julia:$LD_LIBRARY_PATH
echo "export PATH=$PWD/bin:$PATH" >> ~/.bashrc
echo "export LD_LIBRARY_PATH=$PWD/lib:$LD_LIBRARY_PATH" >> ~/.bashrc
echo "export LD_LIBRARY_PATH=$PWD/lib/julia:$LD_LIBRARY_PATH" >> ~/.bashrc

# Setup IJulia and a few packages that we'll be using lots
julia -e 'using Pkg; Pkg.add(["IJulia","Weave","NBInclude"])'

# Create ssh-keys
ssh-keygen -t rsa -b 4096  # follow prompts, default location should be ok
cat ~/.ssh/id_rsa.pub
```

- If this is your first time using git, then enter something for your name and email (you may wish to use your github id rather than your real name, and a non-email address like nobody@nowhere.org).

```shell
git config --global user.email "nobody@nowhere.org"
git config --global user.name "Your Github Id"
```

- Authorize your ssh-keys on GitHub, following [these instructions](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/#platform-linux) but manually copying the key rather than using xclip (i.e., starting from step 2)
- Shutdown the session and close the browser window/tab with the ACI Interactive Desktop
- Go back to the "My Interactive Sessions" tab in the ACI Portal, click "Delete" for this Sessions and confirm.

---
<a id="start-jupyter"></a>
### Start a Jupyter notebook session on ACI
Each time in the future you want to start a Jupyter notebook session on ICDS-ACI

- Browse to portal.aci.ics.psu.edu
- Login (if necessary)
- Click _Interactive Apps_ on top menu
- Choose _Jupyter Notebook_
    + Select:
        - Anaconda version: 5.0.1-3.6.3
        - Allocation: Open
        - Number of hours: 1 hour
        - Node type: ACI-i
    + Click _Launch_
    + Wait while your job starts
- Once the _Connect to Jupyter Notebook Server_ button appears, click it
    + Near the upper right, there's a _New_ button, from which you can create a new blank notebook or access a terminal or text editor.  By default, Python will be the only language avaliable.  It is possible to connect other languages to Jupyter.  See (#setup-julia) for info on setting up Julia.
    + If you'd like to create a blank notebook, then choose _New.Julia 1.0.2_ (or whatever kernel you like and have installed)
    + A new browser tab should open where you can work with a notebook interactively.
    + Do your work, remembering to save your notebook after key edits and before you quite.
- When you're done, close notebook tabs and click logout in upper right (of the Jupyter server session).
- Go back to the "My Interactive Sessions" tab in the ACI Portal, click "Delete" for this Sessions and confirm.

---
<a id="clone-repo"></a>
### Clone your github repository to begin a new project

- Request a Jupyter notebook session on ACI (see [above](#start-jupyter))
- While waiting for it to start, let's get the url for the repo to be cloned.
    + Navigate to the github repository you'll be using.
    + Click _Clone or download_.
    + If it says "Clone with https", click "Use ssh".
    + Click the clipboard icon to copy the url onto your clipboard
- Return to your browser tab with "My Interactive Sessions".
- Hopefully, there's now a _Connect to Jupyter Notebook Server_ button. Click it
- Go to the newly opened tab, you'll have a Jupyter Notebook Server.
- Find _New_ button and choose _Terminal_
- In the new terminal tab, clone your github repo by running

```shell
git clone REPO_URL  # where REPO_URL is what you'll paste from the clipboard
```
- Change into the directory that was created for the repository (we'll call REPO_DIR) and setup all the packge dependancies required.

```shell
cd REPO_DIR
julia -e 'using Pkg; Pkg.activate("."); Pkg.instantiate(); '
```
- Go back to the browser tab with your Jupyter notebook server running.
- Click the directory name of the repository that you just installed.
- Open a Jupyter notebook (file ending in .ipynb) in that repo, or use the _New_ button to create a new one.
- Do your work in the Jupyter notebook.
- When you're done with a notebook, save it and close the tab.

---
