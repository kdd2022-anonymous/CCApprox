# CCApprox

**[Results of Experiments](out/Results/)**

**[Precomputed cores and core information](out/Results/CoreInfo)** 

**Usage of Code:**

1. Clone this repository and navigate into *CCApprox* folder: ```git clone && cd CCApprox```
2. Create folders *GraphData* and *ExternalLibraries* in the parent folder of *CCApprox*: ```mkdir ../GraphData && mkdir ../ExternalLibraries```
3. Move precomputed cores to the *GraphData* folder: ```cp -a out/Results/CoreInfo/. ../GraphData/``` 
4. Unpack the slightly modified SNAP 6.0 library to the right place: ```unzip Snap-6.0.zip -d ../ExternalLibraries/```(the original version can be found [here](http://snap.stanford.edu/releases/Snap-6.0.zip)
5. Download the graphs from http://snap.stanford.edu/data/index.html and save unpacked *.txt* in the *GraphData* folder
6. Create build inside *CCAprox* folder and compile:
   ```mkdir build && cd build && cmake .. && make -j 4```
7. Convert the graphs: ```./ConvertGraphs```
8. Compile and run the executables:
   1. ```./ExpSamplingRuntime``` for sampling runtime experiment
   2. ```./ExpSamplingQuality``` for sampling quality experiment
   3. ```./ExpClosureRuntime``` for closure runtime experiment
   4. ```./ExpExactCore``` for exact core computation
    
       | Optional Arguments | ```-i```  | ```-t```  | ```--generators``` | ```--generator_seed``` | ```--core_iterations``` | ```--max_nodes``` | ```--max_edges``` |
       | :---:   | :-: | :-: | :------------: | :-----------------: | :------------------: | :------------: | :------------: |
       | Seconds | input path | thread num | generator number | generator seed | iterations of the core | max graph size | max graph edges |
   5. ```./ExpApproxCore``` for approximate core computation
   
       | Optional Arguments | ```-i```  | ```-o```  | ```-t```  | ```--generators``` | ```--generators_end```| ```--generators_step``` | ```--generator_seed``` | ```--threshold``` | ```--threshold_end``` | ```--threshold_step``` | ```--core_iterations```  | ```--samples``` | ```--sample_seed```  | ```--max_nodes``` | ```--max_edges``` |
       | :---:   | :-: | :-: | :-: | :------------: | :-----------------: | :------------------: | :------------------: | :------------------: | :------------------: | :------------------: | :------------------: | :------------: | :------------: | :------------: | :------------: |
       | Seconds | input path | output path | thread num | generator first size | generator last size | generator step size | generator seed | threshold smallest size | threshold largest size | threshold step | iterations of the core | number of samples | sample seed | max graph size | max graph edges |
       
       *Grid Search*
    
       ```./ExpApproxCore -i ../../GraphData/RealWorld/ --generators 5 10 100 500 1000 --threshold 0.01 0.02 0.03 0.04 0.05 0.06 0.07 0.08 0.09 0.1 0.15 --threads 2 --outer_loop 0 --small_graphs --no_tree --file_name grid_search_small```
    
       ```./ExpApproxCore -i ../../GraphData/RealWorld/ --generators 5 10 100 500 1000 --threshold 0.01 0.02 0.03 0.04 0.05 0.06 0.07 0.08 0.09 0.1 0.15 --threads 3 --outer_loop 0 --large_graphs --no_tree --file_name grid_search_large```
    
       *Large Graphs*
    
       ```./ExpApproxCore -i ../../GraphData/RealWorld/ --generators 5 10 --threshold 0.01 0.02 --threads 2 --outer_loop 0 --save_load_samples --no_tree --no_core --file_name large_graphs```
      
       *Iterative Approx*
   
       ```./ExpApproxCore -i ../../GraphData/RealWorld/ --generators 10 --threshold 0.01 --threads 2 --outer_loop 1 --no_tree --small_graphs --file_name iteration_1_small```
      
       ```./ExpApproxCore -i ../../GraphData/RealWorld/ --generators 10 --threshold 0.1 --threads 2 --outer_loop 1 --small_graphs --no_tree --file_name iteration_2_small```
    
       ```./ExpApproxCore -i ../../GraphData/RealWorld/ --generators 10 --threshold 0.25 --threads 2 --outer_loop 1 --small_graphs --no_tree --file_name iteration_3_small```
    
       ```./ExpApproxCore -i ../../GraphData/RealWorld/ --generators 10 --threshold 0.1 --threads 2 --outer_loop 2 --small_graphs --no_tree --file_name iteration_4_small```
    
       ```./ExpApproxCore -i ../../GraphData/RealWorld/ --generators 10 --threshold 0.25 --threads 2 --outer_loop 2 --small_graphs --no_tree --file_name iteration_5_small```
    
       ```./ExpApproxCore -i ../../GraphData/RealWorld/ --generators 10 --threshold 0.01 --threads 3 --outer_loop 1 --no_tree --large_graphs --file_name iteration_1_large```
    
       ```./ExpApproxCore -i ../../GraphData/RealWorld/ --generators 10 --threshold 0.1 --threads 3 --outer_loop 1 --large_graphs --no_tree --file_name iteration_2_large```

       ```./ExpApproxCore -i ../../GraphData/RealWorld/ --generators 10 --threshold 0.1 --threads 3 --outer_loop 1 --large_graphs --no_tree --file_name iteration_2_large```
     
       ```./ExpApproxCore -i ../../GraphData/RealWorld/ --generators 10 --threshold 0.25 --threads 3 --outer_loop 1 --large_graphs --no_tree --file_name iteration_3_large```
    
       ```./ExpApproxCore -i ../../GraphData/RealWorld/ --generators 10 --threshold 0.1 --threads 3 --outer_loop 2 --large_graphs --no_tree --file_name iteration_4_large```

       ```./ExpApproxCore -i ../../GraphData/RealWorld/ --generators 10 --threshold 0.25 --threads 3 --outer_loop 2 --large_graphs --no_tree --file_name iteration_5_large```
