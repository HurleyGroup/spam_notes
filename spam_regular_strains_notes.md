### Notes on spam-regularStrains
### Arthur Ding, July 2019

- set up argument parser 
- load tsv from correlation
- get dimensions of data field 
- find node spacing based on coordinates from tsv 
- 2D field or 3D?
- mask if requested
- correct input F field if requested (??)
- set strain mode (either small strains or large strains)
- choose to output either only strain field or also decomposition of rotation tensor and displacement gradient tensor (F) 
- call spam.mesh.structured.regularStrain to calculate strains 
    - input displacement field (Phi field), node spacing, options for large strains and outputting only strain    
- separate strain components  
- save strain fields as tiffs and/or vtks if requested
