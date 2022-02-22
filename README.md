# CCApprox

**[Results of Experiments](out/Results/)**

**[Precomputed cores and core information](out/Results/CoreInfo/)** 

**Usage of Code:**

1. Clone this repository and navigate into *CCApprox* folder: ```git clone https://github.com/kdd2022-anonymous/CCApprox.git && cd CCApprox```
2. Create folders *GraphData* and *ExternalLibraries* in the parent folder of *CCApprox*: ```mkdir ../GraphData && mkdir ../ExternalLibraries```
3. Move precomputed cores to the *GraphData* folder: ```cp -a out/Results/CoreInfo/. ../GraphData/``` 
4. Unpack the slightly modified SNAP 6.0 library to the right place: ```unzip Snap-6.0.zip -d ../ExternalLibraries/```(the original version can be found [here](http://snap.stanford.edu/releases/Snap-6.0.zip)
5. Download the graphs from http://snap.stanford.edu/data/index.html and save unpacked *.txt* in the *GraphData* folder
6. Create build inside *CCAprox* folder and compile:
   ```mkdir build && cd build && cmake .. && make -j 4```
7. Convert the graphs: ```./ConvertGraphs```
8. Compile and run the executables:
   1. ```./ExpSamplingRuntime``` for sampling runtime experiment (output is found in *out/Results/Closure/*)
   2. ```./ExpSamplingQuality``` for sampling quality experiment (output is found in *out/Results/Sampling/*)
   3. ```./ExpClosureRuntime``` for closure runtime experiment   (output is found in *out/Results/Sampling/*)
   4. ```./ExpApproxCore``` for approximate core computation with parameters used for the results, see below (output is found in *out/Results/Approximation/*)    
   
      *Grid Search*
    
       ```./ExpApproxCore -i ../../GraphData/ --generators 5 10 100 500 1000 --threshold 0.01 0.02 0.03 0.04 0.05 0.06 0.07 0.08 0.09 0.1 0.15 --threads 2 --outer_loop 0 --small_graphs --no_tree --file_name grid_search_small```
    
       ```./ExpApproxCore -i ../../GraphData/ --generators 5 10 100 500 1000 --threshold 0.01 0.02 0.03 0.04 0.05 0.06 0.07 0.08 0.09 0.1 0.15 --threads 3 --outer_loop 0 --large_graphs --no_tree --file_name grid_search_large```
      
       *Iterative Approx*
   
       ```./ExpApproxCore -i ../../GraphData/ --generators 10 --threshold 0.01 --threads 2 --outer_loop 1 --no_tree --small_graphs --file_name iteration__small```
    
       ```./ExpApproxCore -i ../../GraphData/ --generators 10 --threshold 0.01 --threads 3 --outer_loop 1 --no_tree --large_graphs --file_name iteration__large```
       
       *Large Graphs*
    
       ```./ExpApproxCore -i ../../GraphData/RealWorld/ --generators 5 10 --threshold 0.01 0.02 --threads 2 --outer_loop 0 --save_load_samples --no_tree --no_core --file_name large_graphs```
      
   
       | Optional Arguments | ```-i```  | ```-o```  | ```--threads```  | ```--generators``` | ```--generator_seed``` | ```--threshold``` | ```--core_iterations```  | ```--samples``` | ```--sample_seed```  | ```--max_nodes``` | ```--max_edges``` |
       | :---:   | :-: | :-: | :-: | :------------: | :-----------------: | :------------------: | :------------------: | :------------: | :------------: | :------------: | :------------: |
       | Seconds | input path | output path | thread num | generator sizes | generator seed | threshold sizes | iterations of the core | number of samples | sample seed | max graph size | max graph edges |
   5. ```./ExpExactCore``` for exact core computation to recalculate the cores for the graphs use: ```./ExpExactCore -i ../../GraphData/ --threads 8 --recalculate```
    
       | Optional Arguments | ```-i```  | ```--threads```  | ```--generators``` | ```--generator_seed``` | ```--core_iterations``` | ```--max_nodes``` | ```--max_edges``` |
       | :---:   | :-: | :-: | :------------: | :-----------------: | :------------------: | :------------: | :------------: |
       | Seconds | input path | thread num | generator number | generator seed | iterations of the core | max graph size | max graph edges |
       
       
       
