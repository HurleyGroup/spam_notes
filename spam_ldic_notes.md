### Notes on spam-ldic
### Arthur Ding, July 2019

- parse arguments using optionsparser.py
- activate parallel processing if requested
- get past mpi selection
- print out settings for DIC from dictionary made of args
- NOTE: "psr" = pixel search range
- load the reference image
- find if reference image is 2D or 3DIC
- if a mask image is specified for the reference image, load it
- set minimum mask volume

- loop through both 3D tiff input images
    - mark last correlation if at end of file sequence
    - assign number to the reference image 
    - decide on output file prefix (either specified or default to basename of input file)
    - for beyond the first correlations
        - do not do initial registration 
        - use previous Ffield for a total correlation
    - load the 2nd input image
    - create grid of correlation points using size of first image and specified node spacing   
    - create PhiField, one 4 x 4 Phi for each node in correlation grid; initialize with 0s
    - if requested, subtract rigid body motion of initial registration from displacments
    - 3 current options for calculating displacement
        1) single image registration 
            - do binning if requested
            - establish registration margin (size of registration area relative to image size; default = 0.1)
            - *run registration*
            - write TSV if requested
        2) use previous registration
            - read Phifile 
                - if one line, is *single-point registration*
                - if multiple lines, is *F field*
                    - set grid of F components to 0, then replace with F field from registration file
                    - check for correction of field (spam.DIC.correctPhiField?)
            - create k-d tree of input F field coordinates?
            - for each note in grid 
                - get distances from current grid points to points of input F field 
                - if at grid point of input F field, copy F from input field to current grid 
                - if not at grid point of input F field, find nearest neighbors, get weight (depending on distance) and fill current grid F value with weighted value  
            - apply registration to mesh (do node-wise)
                - copy registration's small F to F of all points 
                - call decomposePhi function to get translation of each point
        3) pixel search
            - call spam.DIC.grid.pixelSearch 
            - call spam.DIC.grid.subPixel 
    - Correlation finished here, write outputs
        - subtract rigid body motion if requested 
        - make TSV if requested 
        - write tiffs if requested 
        - write vtk if requested 
- not sure about final elif statement about mpi
        
  
