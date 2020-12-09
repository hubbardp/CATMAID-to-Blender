CATMAID-to-Blender
==================

Plugin for [Blender](http://www.blender.org "Blender Homepage") to interface
with [CATMAID](https://github.com/catmaid/CATMAID "CATMAID Repo") servers,
request and analyze data. Tested with Blender 2.79 and CATMAID 2020.02.15

## Important notice
This plugin still works for the time being but is not actively developed at the moment.
You are welcome to open an issue or contact me directly if you run into problems
but I highly recommend you check out [pymaid](https://github.com/schlegelp/pymaid)
and [navis](https://github.com/schlegelp/navis) which - in combination -
let you import neurons programmatically into Blender
(see the [tutorials](https://navis.readthedocs.io/en/latest/source/gallery.html)).
These package also work with Blender >=2.8 while this plugin doesn't.

## Installation:
First download [CATMAIDImport.py](https://raw.githubusercontent.com/schlegelp/CATMAID-to-Blender/master/CATMAIDImport.py), then:

#### Option A:
1. Directly place CATMAIDImport.py in \Blender\...\scripts\addons
2. Start Blender -> **File** -> **User Preferences** -> **Addons** -> Search for **CATMAIDImport** addon
3. Activate the script by ticking the check box and click **Save User Settings** (see [here](http://wiki.blender.org/index.php/Doc:2.6/Manual/Extensions/Python/Add-Ons) for more detailed description)

#### Option B:
1. Start Blender -> **File** -> **User Preferences** -> **Addons** -> **Install from File** and select CATMAIDImport.py
2. Activate by ticking check box and click **Save User Setting**

#### Dependencies:
None! [Blender](http://www.blender.org "Blender Homepage") for Windows and MacOS brings its own Python distribution and the plugin is written such that it works (mostly) without any external libraries.

#### Optional Python packages:
On Windows/MacOs:
- [scipy](https://www.scipy.org/) (will increase performance for clustering).

On Linux:
- [numpy](http://www.numpy.org/) (without numpy, functionality will be limited).
- [scipy](https://www.scipy.org/) (will increase performance for clustering).

There are several ways to install additional packages for Blender's built-in Python. The easiest way is probably this:

- Download pip's [get-pip.py](https://pip.pypa.io/en/stable/installing/) and save e.g. in your downloads directory
- Run [get-pip.py](https://pip.pypa.io/en/stable/installing/) from Blender Python console:

```python
with open('/Users/YOURNAME/Downloads/get-pip.py') as source_file:
    exec(source_file.read())
```

- Then use pip to install any given package. Here, we install as Scipy an example:
```python
import pip
pip.main(['install','scipy'])
```

**There appears to be a bug with macOS 10.12 Sierra which makes above steps fail if run from within Blender.** In that case try:
1. Make sure Blender is in your Applications folder
2. Right click on Blender icon -> **Show Package Contents**
3. Navigate to **Contents/Resources/2.78/python/bin** and run **python3.5m** by drag&dropping it into a Terminal
4. Try above steps from the Terminal

## Before First Use:
Open **File** -> **User Preferences**, navigate to **Add-ons** -> **CATMAIDImport** and change **CATMAID Server URL** in **preferences** to your server. I also recommend saving your credentials for convenience.

The CATMAID API authorizes requests using an **API token** tied to user account instead of a username and password.
For Information on how to retrieve your Token look [here](http://catmaid.github.io/dev/api.html#api-token).

![server_url](https://cloud.githubusercontent.com/assets/7161148/13985056/9b915b22-f0fa-11e5-8b8f-ecac97405708.PNG)

## Quickstart Guide:
Import/Export panel will show up under the **Scene** tab in the **Properties** windows

![import_panel](https://cloud.githubusercontent.com/assets/7161148/23852692/fafcf71c-07e0-11e7-9e64-69ecdc3a3af0.png)

- Functions (e.g. Retrieving skeletons/connectors) that need you to be logged into your CATMAID server will be grayed-out until you did so by hitting 'Connect 2 CATMAID'
- Skeletons can be retrieved by their skeleton ID, by annotations or based on connectivity (Retrieve Partners)
  - Important side node: in order to identify cell bodies, the script searches for nodes with a radius > 10
- Once imported, skeleton/connector data can be readily exported to vector graphics (SVG) with a broad range of options (e.g. coloring, filters, scaling). Look at lower left panel when exporting for these options.

![export_options](https://cloud.githubusercontent.com/assets/7161148/5356716/bf994da4-7f9f-11e4-8e10-c5c628baab47.PNG)

## Tutorials:
Please check out the Github [Wiki](https://github.com/schlegelp/CATMAID-to-Blender/wiki) for additional information and tutorials.

## Examples:

#### 1. Color neurons by similarity and export to vector graphic (SVG)
<img src="https://cloud.githubusercontent.com/assets/7161148/14020628/465496f4-f1d8-11e5-899b-5bb1f6baf8b0.png" width="650">


#### 2. Group postsynaptic sites based on what presynaptic neuron they connect to
<img src="https://cloud.githubusercontent.com/assets/7161148/14020676/7df96468-f1d8-11e5-9f04-aba115112890.png" width="650">

#### 3. Check out [Schlegel et al., 2016 (eLife)](https://elifesciences.org/content/5/e16799) for more examples.


## License:
This code is under GNU GPL V3

## Acknowledgments and how to cite:

#### General:
Please cite [Schlegel et al., 2016 (eLife)](https://elifesciences.org/content/5/e16799) if you use the plugin in your publication.

#### Specific Methods:
Some functions available within the plugin are based on/derived from previously published methods. Please cite the original papers if you make use of these specific methods.

1. **Comparison of neurons based on morphology**: Cell. 2013 Dec 19;155(7):1610-23. doi: 10.1016/j.cell.2013.11.025.
*A bidirectional circuit switch reroutes pheromone signals in male and female brains.*
Kohl J, Ostrovsky AD, Frechter S, Jefferis GS.
http://www.cell.com/abstract/S0092-8674(13)01476-1
2. **Comparison of neurons based on connectivity**: Science. 2012 Jul 27;337(6093):437-44. doi: 10.1126/science.1221762.
*The connectome of a decision-making neural network.*
Jarrell TA, Wang Y, Bloniarz AE, Brittin CA, Xu M, Thomson JN, Albertson DG, Hall DH, Emmons SW.
http://science.sciencemag.org/content/337/6093/437.long
3. **Comparison of neurons based on synapse distribution**: eLife. doi: 10.7554/eLife.16799
*Synaptic transmission parallels neuromodulation in a central food-intake circuit.*
Schlegel, P., Texada, M. J., Miroschnikow, A., Schoofs, A., Hückesfeld, S., Peters, M., … Pankratz, M. J.
https://elifesciences.org/content/5/e16799
