# ARCHER2 Known Issues

This section highlights known issues on ARCHER2, their potential
impacts and any known workarounds. Many of these issues are under
active investigation by HPE Cray and the wider service.

## Singularity and CMake
The issue concerns the building of a cmake-compiled code in bind mode in
Singularity containers. This fails because CMake 3.x, running within the
container on a UAN, cannot find the MPI libraries (cray-mpich) on the host
despite the correct paths having been provided.

## Research Software
There are several outstanding issues for the centrally installed Research Software:
- **ChemShell and PyChemShell** are not yet available. We are working with the code developers to address this.
- **Climate Data Operators (CDO) and NCAR Command Language (NCL)** are not yet available, due to issues with dependencies. An investigation is on-going.
- **Paraview** is not yet available. We hope to provide a suitable installation in the near future.
- **VMD** is not yet available. We hope to provide a suitable installation in the near future.
- **PLUMED** is not yet available. Currently, we recommend affected users to install a local version of the software.

Users should also check individual software pages, for known limitations/ caveats, for the use of software on the Cray EX platform and Cray Linux Environment.

## `stat-view` not working
The `stat-view` utility from the `cray-stat` module does not currently
work due to missing dependencies within the HPE Cray software stack. If you 
try to use the tool, you will see errors similar too:

```
auser@uan01:~> module load cray-stat
auser@uan01:~> stat-view
Traceback (most recent call last):
File "/opt/cray/pe/stat/4.7.1/lib/python3.6/site-packages/STATview.py", line 60, in <module>
import xdot
ModuleNotFoundError: No module named 'xdot'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
File "/opt/cray/pe/stat/4.7.1/lib/python3.6/site-packages/STATmain.py", line 73, in <module>
raise import_exception
File "/opt/cray/pe/stat/4.7.1/lib/python3.6/site-packages/STATmain.py", line 40, in <module>
from STATGUI import STATGUI_main
File "/opt/cray/pe/stat/4.7.1/lib/python3.6/site-packages/STATGUI.py", line 37, in <module>
import STATview
File "/opt/cray/pe/stat/4.7.1/lib/python3.6/site-packages/STATview.py", line 62, in <module>
raise Exception('STATview requires xdot\nxdot can be downloaded from https://github.com/jrfonseca/xdot.py\n')
Exception: STATview requires xdot
xdot can be downloaded from https://github.com/jrfonseca/xdot.py
```

## Issues with RPATH for non-default library versions
When you compile applications against non-default versions of libraries within the HPE
Cray software stack and use the environment variable `CRAY_ADD_RPATH=yes` to try and encode
the paths to these libraries within the binary this will not be respected at runtime and
the binaries will use the default versions instead.
