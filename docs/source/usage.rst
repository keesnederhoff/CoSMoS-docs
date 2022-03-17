Getting started
=====


Installation
------------

To use CoSMoS, first make a check-out with, for example, TortoiseSNVN, of the CoSMoS and other related code. Scripts are hosted on the Deltares' repository called Open Earth Tools. 

You will need the following folders:
1. https://svn.oss.deltares.nl/repos/openearthtools/trunk/python/applications/cosmos
2. https://svn.oss.deltares.nl/repos/openearthtools/trunk/python/applications/delft3d
3. https://svn.oss.deltares.nl/repos/openearthtools/trunk/python/applications/DeltaShell
4. https://svn.oss.deltares.nl/repos/openearthtools/trunk/python/applications/tropical_cyclones
5. https://svn.oss.deltares.nl/repos/openearthtools/trunk/python/applications/xbeach

Secondly, make an Python environment in, for example, Anaconda such that the Python interpreter, libraries and scripts installed into it are isolated from the rest. 
>>> conda env create -f d:\checkouts\Python\OpenEarthTools\cosmos\environment_cosmos.yml


Adding to path
----------------

Before you can run CoSmoS, you will have to add it your path. You can use you can alter the ``cosmos_add_paths()`` function. An example code is attached below:

>>> # Import relevant libraries
>>> import sys
>>> import os
>>> 
>>> # Paths needs from cosmos
>>> mainpath    = r'd:\\checkouts\\Python\\OpenEarthTools\\cosmos\\'     # change this one
>>> variations  = ["cosmos", "delftdashboard", "bathymetry_database","gui_toolbox", "misc", "meteo", "delft3dfm", "hurrywave", "tiling", "sfincs"]
>>> sys.path.append(mainpath)
>>> for variation in variations:
>>>     path_file = os.sep.join([mainpath, variation])
>>>     #print(os.stat(path_file))
>>>     if os.path.isdir(path_file):
>>>         sys.path.append(path_file)
>>>     else:
>>>         print('path not found - ' + path_file) 
>>> # Other (extra) paths needed
>>> path_file = r'd:\\checkouts\\Python\\OpenEarthTools\\deltashell\\applications\\CoDeS\\CoDeS_2.0\\Tide\\pytides\\'
>>> if os.path.isdir(path_file):
>>>     sys.path.append(path_file)
>>> else:
>>>     print('path not found - ' + path_file) 


Running a simulation
----------------

Once CoSMoS is installated and added to your path you can start a simulation. You can use you can use the ``run_cosmos()`` function. An example code is attached below:

>>> from cosmos import cosmos
>>> # Run cosmos_addpaths.py before executing run_cosmos.py
>>> main_path       = "d:\\cosmos"
>>> scenario_name   = "hurricane_michael_gfs_spw"
>>> cosmos.initialize(main_path, scenario_name)
>>> # Run cosmos
>>> cosmos.run(mode="single_shot",
>>>            run_models=True,
>>>            make_flood_maps=True,
>>>            make_wave_maps=True,
>>>            get_meteo=True,
>>>            upload_data=False,
>>>            make_figures=True,
>>>            hurrywave_exe_path=r'd:\checkouts\Hurrywave\trunk\hurrywave\x64\Release',
>>>            sfincs_exe_path=r'd:\checkouts\SFINCS\branches\subgrid_openacc_11\sfincs\x64\Release',
>>>            ensemble=False)