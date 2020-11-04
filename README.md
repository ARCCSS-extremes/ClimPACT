
# <p align="center">Climpact</p>

##  What is Climpact?
  
Climpact is an R package that calculates [indices of daily climate extremes](https://climpact-sci.org/indices/). It can read 
data for a single site (e.g. a weather station) in the form of a text file or gridded data (e.g. from a climate model) in the form of netCDF files. This software directly builds off the R packages climdex.pcic and climdex.pcic.ncdf, developed by the Pacific Climate Impacts Consortium ([PCIC](https://www.pacificclimate.org/)). 

*If you want to calculate these indices from text files then you **DO NOT** need to install this software, instead go to the [Climpact website](https://climpact-sci.org/get-started/) to calculate these indices online.*
  
  
##  Where can I get Climpact?
  
When calculating the indices for station data Climpact can be accessed [online](https://climpact-sci.org/get-started/). Climpact is also available for download at [this github site](https://github.com/ARCCSS-extremes/climpact) for users who also wish to calculate the indices on gridded data. The software runs on Windows, Linux and MacOS, though only on Linux and MacOS for gridded calculations.


## How do I install Climpact?

If you do not wish to use the [online version](https://climpact-sci.org/get-started/) of Climpact then you can install it locally noting the following software requirements:  
* R version 3.3 or later. You will need administrator privileges on your computer or the ability to install R packages.
* Linux users wanting to calculate indices on gridded data require the *PROJ4* development files (libproj-dev package on Ubuntu) and the [*udunits*](https://www.unidata.ucar.edu/software/udunits/) development files (libudunits2-dev package on Ubuntu).



1. Download and extract [this file](https://github.com/ARCCSS-extremes/climpact/archive/master.zip) to your computer.
   This will create a directory named "climpact-master".

2. Install the required R-packages. This step can take several minutes and only needs to be done once.

   In Windows: open R and select "File->Change dir..." and select the
   climpact-master directory created in step 1. Then type;  

   *source('server/climpact.master.installer.r')*

   In Linux/MacOS: in a terminal window navigate to the climpact-master directory created in
   step 1, then open R (by typing *R* at the command line) and type;  

   *source('server/climpact.master.installer.r')*

   You may be asked whether you would like to make a personal library, in 
   most cases the answer should be 'yes'. Once complete, quit R by typing
   *q()*. 
   

Video tutorial on how to install R in Windows
-> https://www.youtube.com/watch?v=a-vnLME6hRQ&t=26s

Video tutorial on how to install ClimPACT in Windows
-> https://www.youtube.com/watch?v=Q7ERKmnpYvo&t=3s


##  How do I start Climpact once I've installed it on my computer?

* In Windows: open R and select "File->Change dir..." and select the 
climpact-master directory created when installing ClimPACT. Then run the 
following two commands;  

*library(shiny)*  
*runApp()* 

* In Linux/MacOS: navigate to the climpact-master directory created in
step 1, then open R (by typing *R* at the command line) in a terminal window and run the following two
commands;  

*library(shiny)*  
*runApp()* 

Follow the on-screen instructions to calculate the Climpact indices.

Video tutorial on calculating indices from a station text file.  
-> 


##  ADVANCED: Calculate indices on netCDF data (Linux/MacOS only)

Warning: Due to an error in the SPEI and SPI package these indices will not be
correct for gridded data IF your data contain missing values (e.g. they are based on remote sensing observations).
    
Warning: Calculating and using the gridded indices requires familiarity with the command line and netCDF files.

1) Navigate to the climpact-master directory created when installing Climpact. Then modify the *climpact.ncdf.wrapper.r* file to suit your needs (see user guide
   for optional parameters to specify). 
   
2) Execute the above script by running *Rscript climpact.ncdf.wrapper.r* from the command line. Depending
   on the size of your data and the number of cores selected, this process
   can take anywhere from one to effectively an infinite number of hours. As a
   yard stick, for a 20 year global ~1x1 degree dataset and a computer with 2 cores you should assign ~30 hours to begin with.

### Notes on netCDF data format:
* Look at the sample netCDF file for guidance in formatting your
  data.
* Files must be CF compliant.
* There must be no 'bounds' attributes in your latitude or 
  longitude variables.
* Your precipitation variable must have units of "kg m-2 d-1",
  not "mm/day". These are numerically equivalent.
* Your minimum and maximum temperature variables must be 
  uniquely named.
* ncrename, ncatted and ncks from the NCO toolset can help 
  you modify your netCDF files.
  http://nco.sourceforge.net/


##  ADVANCED: Calculate thresholds on netCDF data from the command line


1) Navigate to the climpact-master directory created when installing Climpact. Then modify the *climpact.ncdf.thresholds.wrapper.r* file to suit your needs (see user guide for guidance on the parameters to specify). 
   
2) Then execute this file by running *Rscript climpact.ncdf.thresholds.wrapper.r* from the command line. Depending
   on the size of your data and the number of cores selected, this process
   can take anywhere from one to many hours.


## ADVANCED: Batch process multiple station files from the command line
  
Software you will need before proceeding:
* R (version 3.3 or later). You will need administrator privileges on your computer or the ability to install R libraries.

1) Navigate to the climpact-master directory created when installing Climpact. 
       
2) From the terminal run the following command, replacing the flags
   with: the folder where your station text files are kept, a metadata file
   containing the file name of each station text file along with relevant 
   station information (see the sample provided), the beginning and end years of the base period, and
   the number of cores to use in processing, respectively. See the user guide
   for more information.
   *Rscript climpact.batch.stations.r ./www/sample_data/ ./www/sample_data/climpact.sample.batch.metadata.txt 1971 2000 2*


##  Common problems

* If you experience trouble installing R packages in Windows, try to disable
  your antivirus software temporarily.
* If you are trying to use the wrapper scripts in Windows anyway, ensure your PATH
  environment variable is changed to include the installation directory of R.


##  Documentation

Documentation exists in the form of this README file, the official Climpact
user guide (available in the *server* folder) as well as the source code.


##  Contact
  
Software issues contact Nicholas Herold : nicholas.herold@unsw.edu.au
 
All other issues contact Lisa Alexander : l.alexander@unsw.edu.au
