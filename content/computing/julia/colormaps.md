+++
title = "Colormaps for PyPlot.jl"
date = "11 August 2018"
type = "page"
hidden = false
weight = 1000

# Creator's Display name
creatordisplayname = "Daniel Carrera"
# Creator's Email
#creatoremail = "hidden at psu dot edu"
# LastModifier's Display name
lastmodifierdisplayname = "Eric Ford"
# LastModifier's Email
#lastmodifieremail = "hidden at psu dot edu"

+++



A group of oceanographers have significantly expanded the list of uniform colormaps available. When the original colormaps were released, the author also released a tool for making uniform colormaps. The oceanographers then "ported" many of the existing colormaps from matplotlib and gave them names that apprently make sense to oceanographers:

https://matplotlib.org/cmocean/


For those of you who use Python, you can install it with "pip install cmocean".

For those of you who use Julia with PyPlot.jl, I write a 5-line script that makes all these colormaps available in Julia:

https://github.com/dcarrera/CmOcean.jl


They even have a colormap called "phase" that steps through all the colours of the rainbow, but is uniform for people with trichromatic vision. Needless to say, it's not suited for black & white printing or colorblind. But it's good that it's there as an option.

