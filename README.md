# statphase2slowvec  

statphase2slowvec.py  

Release v1.0.0 from October 13, 2022, is archived under  
https://zenodo.org/record/7195885#.Y0rf0UxBxaQ with DOI 10.5281/zenodo.7195885  
[![DOI](https://zenodo.org/badge/550870905.svg)](https://zenodo.org/doi/10.5281/zenodo.7195884)  

https://doi.org/10.5281/zenodo.7195885  

Licenced under the EUPL (European Union Public Licence)  
https://joinup.ec.europa.eu/collection/eupl/eupl-text-eupl-12  

Steven J Gibbbons  
June 14, 2021 (NGI)  

Needs os, sys, argparse, numpy, geographiclib, math, obspy  

Single standalone python code which takes a single ASCII file of the format  

```
Station_Name   Phase_Name   Station_Lat  Station_Lon
```

together with a reference coordinate for the source,
and it will write out a file containing the corresponding lines

```
Station_Name   Phase_Name   Station_Lat  Station_Lon  Ref_Lat  Ref_Lon   Sx_outgoing  Sy_outgoing
```

where Sx and Sy are the East-West and the North-South horizontal slowness vectors at the  
seismic source given by Ref_Lat Ref_Lon with units (s/km) with respect to the AK135 model  
(Kennett et al., 1995).  

For example, we consider the Hukkakero explosion site in Northern Finland
(see Gibbons et al., 2020).  

We use the reference coordinates  
latitude 67.93590 and longitude 25.83491.  

We want to calculate the slowness vectors for the outgoing wavefront for the first arriving regional P
phase and the first arriving regional S phase for the 6 stations used by the study Gibbons et al. (2020).  

So our input file is as follows:  

```
ARE0   P1   69.53490  25.50580  
ARE0   S1   69.53490  25.50580  
KEV    P1   69.75530  27.00670  
KEV    S1   69.75530  27.00670  
SGF    P1   67.44211  26.52611  
SGF    S1   67.44211  26.52611  
LP34   P1   67.26574  28.12528  
LP34   S1   67.26574  28.12528  
LP53   P1   68.08434  27.18877  
LP53   S1   68.08434  27.18877  
LP61   P1   67.91408  23.93216  
LP61   S1   67.91408  23.93216
```

(call it, for example Finland_phaselist.txt).  

If we call the program as follows:  

```
python ../statphase2slowvec.py  \  
          --reflat  67.93590   \  
          --reflon  25.83491   \  
          --phaselistfile Finland_phaselist.txt   \  
          --outfile       Finland_ak135_slovecs.txt
```

then this should generate the following ASCII file:  

```
ARE0  P1        69.53490   25.50580  67.93590   25.83491   -0.00888570    0.12337091  
ARE0  S1        69.53490   25.50580  67.93590   25.83491   -0.01594664    0.22140645  
KEV   P1        69.75530   27.00670  67.93590   25.83491    0.02687697    0.12073203  
KEV   S1        69.75530   27.00670  67.93590   25.83491    0.04823417    0.21666916  
SGF   P1        67.44211   26.52611  67.93590   25.83491    0.08181667   -0.15176232  
SGF   S1        67.44211   26.52611  67.93590   25.83491    0.13714934   -0.25439928  
LP34  P1        67.26574   28.12528  67.93590   25.83491    0.13871543   -0.10238026  
LP34  S1        67.26574   28.12528  67.93590   25.83491    0.23252879   -0.17162010  
LP53  P1        68.08434   27.18877  67.93590   25.83491    0.16493699    0.05021592  
LP53  S1        68.08434   27.18877  67.93590   25.83491    0.27648398    0.08417697  
LP61  P1        67.91408   23.93216  67.93590   25.83491   -0.17239066   -0.00260066  
LP61  S1        67.91408   23.93216  67.93590   25.83491   -0.28897858   -0.00435949
```

(with the name *Finland_ak135_slovecs.txt*)


#References  

Gibbons, S.J., Kvaerna, T., Tiira, T., Kozlovskaya, E., 2020.  
A benchmark case study for seismic event relative location,  
Geophys J Int, 223, 1313-1326  
https://doi.org/10.1093/gji/ggaa362  

Kennett, B.L.N. Engdahl, E.R. & Buland R., 1995.  
Constraints on seismic velocities in the Earth from travel times,  
Geophys J Int, 122, 108-124  
https://doi.org/10.1111/j.1365-246X.1995.tb03540.x  
