# Energy Exascale Earth System Model (E3SM) Version 2 U-MICH Version

E3SMv2 with modified longwave radiation scheme (ice scattering + realistic surface emissivity) by Prof. Xianglei Huang's group at U-Michigan.

**Note: The master branch is the original E3SMv2 model. Please clone the corresponding branches listed below to get access to the modified model.**

## Contribute Authors

- Yi-Hsuan Chen (yihsuan@umich.edu)
- Xiuhong Chen (xiuchen@umich.edu)
- Xianwen Jing (xianwen@umich.edu)
- Wuyin Lin (wlin@bnl.gov)
- Chongxing Fan (cxfan@umich.edu)

## Available Branches

- `master`: The original E3SMv2 code. The starting point is indeed a version 137 commits behind the master branch.
- `cxfan/master/test`: The original E3SM code that we started developing on.
- `cxfan/UMRad`: Our UMRad modification on the radiation scheme. 
  - Two/four-stream radiative solver (flag_rtr2)
	- MC6 ice cloud LW optical scheme (flag_mc6)
  - CAM radiation interface change (radiation.F90; flag_emis and flag_scat)
  - Surface emissivity translational layer in CAM and ELM
  - Bug fixes including non-BFB issues. COSP is turned off here to avoid a bug that has been fixed in the later branches.
- `cxfan/wuyin-1-1`: Our UMRad modification + Wuyin’s 1-1 improvement.
  - The translational layer code has been migrated to a new file: surface_emis_mod.F90. Except for the location change, everything remains intact.
- `cxfan/wuyin-1-2`: Our UMRad modification + Wuyin’s 1-2 improvement.
  - Additionally, the surface emissivity dataset is read once a month rather than every time step.
	- The emissivity file name can be specified in the namelist, rather than hardcoded in the source.
	- COSP is switched on.
- `cxfan/wuyin-2-0`: Our UMRad modification + Wuyin’s 2-0 improvement.
	- Additionally, the surface emissivity dataset is remapped to the model grid. The model now directly reads in the remapped dataset instead of doing the nearest match.
	- The emissivity file name can be specified in the namelist, rather than hardcoded in the source.
	- COSP is switched on.
- `cxfan/wuyin-1-2.v2`: Our UMRad modification + Wuyin’s 1-2 improvement + E3SM official v2 tag.
	- The branch has been merged with the official v2 tag.
- `cxfan/wuyin-2-0.v2`: Our UMRad modification + Wuyin’s 2-0 improvement + E3SM official v2 tag.
	- The branch has been merged with the official v2 tag.
- In `cxfan/wuyin-1-2` and `cxfan/wuyin-2-0`, the commits of our modification are grouped together, and it is instructive to read the commits in the chronological order.
- In `cxfan/wuyin-1-2.v2` and `cxfan/wuyin-2-0.v2`, the commits of our modification are mixed with other commits from the E3SM team. They are recommended for production uses.

## Test Results

The following speed tests are performed on Cori using the L pelayout (101 nodes, 6464 CPUs, 1 thread), and each test produces 6-month climatology.

| Model | Description | Wallclock Time | SYPD | Cost (pehrs/yr) |
| --- | --- | --- | --- | --- |
| UMRad.v2.LR.hist_full | Xianwen's code with all flags turned on | 3:02:38 | 4.00 | 38753.37 |
| UMRad.1-2.v2.LR.hist_full | Wuyin's new I/O that reads the emissivity dataset once a month | 2:10:02 | 5.68 | 27295.19 |
| UMRad.2-0.v2.LR.hist_full | Wuyin's new I/O that reads the remapped emissivity dataset instead of performing nearest matching | 1:57:04 | 6.46 | 24024.72 |
| master.v2.LR.hist | The master branch of E3SMv2 | - | 6.07* | 25547.67* |

* Estimated via a 10-day run, should be a lower bound for SYPD

For more information on the details of the modification, please refer to [this repo](https://github.com/Huang-Group-UMICH/E3SM_v2_alpha) or contact me directly.


[![E3SM Logo](https://e3sm.org/wp-content/themes/e3sm/assets/images/e3sm-logo.png)](https://e3sm.org)

Energy Exascale Earth System Model (E3SM)
================================================================================

E3SM is a state-of-the-art fully coupled model of the Earth's climate including
important biogeochemical and cryospheric processes. It is intended to address
the most challenging and demanding climate-change research problems and
Department of Energy mission needs while efficiently using DOE Leadership
Computing Facilities.  

DOI: [10.11578/E3SM/dc.20210927.1](http://dx.doi.org/10.11578/E3SM/dc.20210927.1)

Please visit the [project website](https://e3sm.org) or our [Confluence site](https://acme-climate.atlassian.net/wiki/spaces/DOC/overview)
for further details.

For questions about the model, use [Github Discussions](https://github.com/E3SM-Project/E3SM/discussions)

Table of Contents 
--------------------------------------------------------------------------------
- [Quick Start](#quickstart)
- [Supported Machines](#supportedmachines)
- [Running](#running)
- [Contributing](#contributing)
- [Acknowledge](#acknowledge)
- [License](#license)

Quick Start
--------------------------------------------------------------------------------
The [Quick Start](https://e3sm.org/model/running-e3sm/e3sm-quick-start/) page 
includes instructions on obtaining the necessary code and input data for model 
setup and execution on a supported machine.

Supported Machines 
--------------------------------------------------------------------------------
E3SM is a high-performance computing application and generally requires a
capable compute cluster to run a scientifically validated case at a useful
simulation speed.

To run E3SM, it is recommended that you obtain time on a 
[Supported Machine](https://e3sm.org/model/running-e3sm/supported-machines/).

Running
--------------------------------------------------------------------------------
Please refer to [Running E3SM](https://e3sm.org/model/running-e3sm/) 
 for instructions on running the model. 

Contributing
--------------------------------------------------------------------------------
Please refer to [Contributing](CONTRIBUTING.md) for details on our code development
process.

Acknowledgement
--------------------------------------------------------------------------------
The Energy Exascale Earth System Model (E3SM) Project should be acknowledged in
publications as the origin of the model using
[these guidelines](https://e3sm.org/resources/policies/acknowledge-e3sm/).

In addition, the software should be cited.  For your convenience,
the following BibTeX entry is provided.
```TeX
@misc{e3sm-model,
	title = {{Energy Exascale Earth System Model (E3SM)}},
	author = {{E3SM Project}},
	abstractNote = {{E3SM} is a state-of-the-art fully coupled model of the {E}arth's 
		climate including important biogeochemical and cryospheric processes.},
	howpublished = {[Computer Software] \url{https://dx.doi.org/10.11578/E3SM/dc.20210927.1}},
	url = {https://dx.doi.org/10.11578/E3SM/dc.20210927.1},
	doi = {10.11578/E3SM/dc.20210927.1},
	year = 2021,
	month = sep,
}
```

License
--------------------------------------------------------------------------------
The E3SM model is available under a BSD 3-clause license.
Please see [LICENSE](LICENSE) for details.

