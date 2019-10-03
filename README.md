# Cartosat-1-DEM-Mosaic
Name of the program: DEMOverlap_mosaic

Title of the manuscript: A novel framework for seamless mosaic of Cartosat-1 DEM scenes

Author details:

1. Rajeshreddy Datla,
Scientist-SE,
Signal processing division, 
Advanced Data Processing Research Institute (ADRIN), 
Indian Space Research Organization (ISRO),
Department of Space, 
Government of India, 
Akbar Road, Tarbund, 
Manovikas Nagar, Secunderabad 500009, India
Telephone number:+919704143731
E-mail:rajesh@adrin.res.in

2. Dr. C Krishna Mohan,
Professor,
Room No. 103, Block - A
Department of Computer Science and Engineering
Indian Institute of Technology Hyderabad
Kandi, Sangareddy - 502285, Telangana (State), India. 


Instructions to use this software:

A. Software with source code:

The complete software with source code is provided in the folder "DEMOverlap_mosaic". It consists of THREE sub-folders, namely,

1) DEMFilterLib: It contains separate functions for the DEM mosaic, namely, Mosaic_Average, Mosaic_Conventional, and Mosaic_Proposed, corresponding to average method, feathering-based blend method and Proposed method, respectively. 
	1.1) Mosaic_Average function: It creates an virtual grid based on the extents of the input DEM scenes and assigns the elevation value to each cell of 		     the grid, by computing the average of the elevation values in the overlapping regions wherever a cell contains more than one elevation value. 		     Finally, gdal_translate is used to crop the result to ROI extent.

 	1.2) Mosaic_Conventional function: It is basically feathering-based blend method. This method considers two inputs at a time for the mosaic, according 			to its nature of the methodology (scalability property). It collects all the input DEM scene filenames in a list and iterates by cascading the 			output generated from the first two inputs with the third input for the	mosaic process. Then, considering the resulted output with fourth 			input for the mosaic and so on. It computes the overlapping region and the valid-data(non-NODATA) cells along the scan and pixel direction for 			every iteration. It derives a weighting mechanism based on the number of valid-data cells and uses these weights in the mosaic process to 			compute a new elevation value. It does not use meta-data of the input scenes. 

	1.3) Mosaic_Proposed: Cartosat-1 mission has a unique path-row referencing scheme. This method makes use of this referencing-scheme which is available 			in the form of meta-data of each input DEM scene. It arranges the input scenes in a hierarchical manner and establishes a sequence. This 			method uses this sequence during mosaic process and creates a seamless mosaic. Hoever, It also computes the overlapping region and the valid-data(non-NODATA) cells along the scan and pixel direction for every iteration. It derives a weighting mechanism based on the number of valid-data cells and uses these weights in the mosaic process to compute a new elevation value.

	
2) DEMFIlterRef (It has function to invoke the mosaic methods)
3) SIPS (Satellite Image Processing System - It reads the tiff into binary form along with the required meta-data population)

All the three mosaic methods use "gdal_translate" command to crop the mosaic output to an ROI extent.



B. Folder sturcture of input and output data:
   Input files must be placed in the folder that denotes a tile, e.g., 64G_E81_N21
   The file name of an input DEM scene has the following naming convention:
     P5008536_1P_20061202_556295, where P5 represents Sensor name followed by 6-digit orbit number,1P represents the payload code follwoed by date in YYYYMMDD format; followed by path(3-digit) and row(3-digit);
     
     
     
C. Usage of this software:
   Create a c++ source project using IDE (e.g., Microsoft visual studio, Netbeans)
   Load the .sln file (solution file) from the IDE. Include the paths of the header files and the lib files in the configuration. First build the DEMFilterLib.cpp to generate DEMFilterLib.lib and use this lib as dependency while building DEMFIlterRef.cpp. 
   The two files are supposed to get generated are: DEMFilterLib.lib and DEMFIlterRef.exe ,after building the corresponding source cpp files.
   
   
   Software can be executed through command prompt also, apart from the IDE, as mentioned below:
   Usage: DEMFIlterRef <inputfolder> <outputfolder> {1 | 2| 3}
  inputfolder: location of the Parent folder of the tile folder(64G_E81_N21)
  output folder: It must have read/write permission.It must be different from the inputfolder.
  {1|2|3}: option 1 for Proposed method; 2 for average method ;3 for conventional feathering-based blend method.
   This software is compiled and executed in Microsoft visual studio 2010.
This software is implemented with an intension to include these methods as static library for better reusage.
