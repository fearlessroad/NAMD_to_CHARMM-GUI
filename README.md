# NAMD to CHARMM-GUI FF Converter
Tutorial for converting NAMD/VMD-generated psf/pdb files to CHARMM PSF/CRD (credit attributed where appropriate to the AMAZING humans who developed these scripts)

To use the CHARMM-GUI FF Converter (current as of Sept. 29, 2021), you need to input a CHARMM-compatible CRD and PSF. 

## 1. Convert PSF/PDB to CHARMM CRD 
  - Use the script from the <a href='https://www.ks.uiuc.edu/Research/vmd/script_library/scripts/write_charmm_crd/'>VMD scripts library</a>, found <a href= 'https://www.ks.uiuc.edu/Research/vmd/script_library/scripts/write_charmm_crd/write_charmm_crd.tcl'>here</a>, written by Mitchell Gleed (mgleed at byu.edu) 2015. (Last accessed Sept 22, 2021)
  - To use with interactive VMD console: 
  ``` 
  vmd -dispdev text
  mol new PSF.psf 
  mol addfile PDB.pdb
  source write_charmm_crd.tcl
  writecharmmcoor "output.crd" 0 "normal"
 ```
Usage Note: Use the "normal" keyword, even if your system > 99,999 atoms. There's a bug in the code where it won't work if you use "expanded" as stated.  
 
2. Generate CHARMM-compatible PSF with PSFGEN
- Generate the psf with psfgen
``` 
psfgen
readmol psf PSF.psf pdb PDB.pdb
writepsf x-plor XPLOR.psf
```
- Add "XPLOR" keyword to the header of the XPLOR.psf:
```
PSF EXT CMAP XPLOR
```
Thanks to the CHARMM-GUI help team, and specifically Jumin Lee and Nathan Kern for instructions here, and Lorenzo Casalino for finding a typo. (Adding the "XPLOR" keyword suddenly made this work??? Whaaat??? Why are there so many secrets?) 
> Note: Until Sept. 29, 2021, 1pm PST, there was a bug in the CHARMM-GUI FF Converter in which it would not accept PSF files with capital letters. We have been informed that this is no longer an issue and you can name the psf file anything you want, e.g., ABBY.psf works. 

## Upload Files to CHARMM-GUI FF Converter
- Your files should now be readable by the FF Converter. If you get an error saying you're missing a residue, you'll need to upload the relevant topology files that contain info for that residue.
- You can now run through the steps and generate input files for GROMACS, AMBER, etc. 

