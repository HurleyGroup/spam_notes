### Notes on spam.mesh.structured.py
### Arthur Ding, July 2019

- as docstring says, structured.py is a set of tools used to manipulate structured meshes 

##### regularStrain function
- compute strain at center of 8-node cell w/linear shape function 
- define # of nodes, # of cells 
- if 2D displacement field is passed, add ficticious layer of nodes and cells with equal displacement to real layer, this way there is no z-strain 
- define coordinates of parent element (8-nodes)
- calculate derivatives of shape functions 
    - local node coordinate divided by weight (in this case, equal weight because node center is equidistant from each node)
- calculate Jacobian to go from local to global
    - 2/nodespacing in x, y, or z
- loop over all cells (3 dimensions, triple nested for loop)
    - check for NaNs
    - for each node in the cell (8 of them)
        - get all components of displacement gradient tensor
            - jacobian times derivative of shape function times displacement value
    - decompose displacement gradient (either large or small strain)
        - output depends on large or small strain 
- return volumetric strain, deviatoric strain, and other values depending on large/small strain calculation
