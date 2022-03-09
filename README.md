# FrequentPatternBasedSearch
# Frequent pattern based serach A case study on the quadratic assignment problem
Accepted in [IEEE Trans. Syst. Man Cybern. Syst. 2022](https://ieeexplore.ieee.org/abstract/document/9240997)

## Requirements

GCC/G++ for Linux

This is the environment for our experiments. 

## Benchmark instances

The link to the popular benchmark instances from QAPLIB.
https://www.opt.math.tugraz.at/qaplib/

## Compiling the program

We already written the `makefile` file. To compile the program, just use 
```
make
```

## Running the program

To perform the program, use 
```
./dmbmaqap instance_name dataset best_known_cost nbr_repeats limit_time
```
The arguments above are necessary, and they mean:
```
instance_name #the file name of an instance
dataset #which dataset the instance is in
best_known_cost #the current best-known cost of the instance
nbr_repeats #the times of runs
limit_time #the upper limit time of a run
```
For example, to run on the instance `sko72` in Linux for 30 times, with a time limit of 3600 s each time
```
./dmbmaqap sko72.dat HARDS 66256 30 3600
```

## The organization of this code

This part is for people who want to build their own methods based on this code.

The core of this code is the `FPBS_v1()` method. In specific, it covers the initialization of the population, frequent pattern mining, offspring construction, the local optimization and the updating of the population.

Before the evolution, the population are initialized by `build_unique_elite()` method which builds k distinct high-quality solutions.

After the population is initialized, the method `mine_frequent_patterns()` is called, which provides the initial frequent patterns as entrance to population evolution.

In each generation, `solution_construct_based_mined_pattern(n,i,child_sol)` and `breakout_local_search(n, flow, dist, child_sol, child_cost, 10000, child_time)` are used to construct a high-quality offspring solution. Then the method `update_pool_unique(n, child_sol, child_cost, child_time,Pop, Pop_costs, PS)` updates the population with the new offspring.

The mining process `mine_frequent_patterns()` wakes up when the population stagnates.

## Building your own method
To modify the method or build your own method based on this code, you can do this by changing the corresponding methods.
Some examples are given below:

To change the way to construct offspring solutions, you can modify the `solution_construct_based_mined_pattern(n,i,child_sol)` method.

To change or improve the local search procedure, you can modify the `breakout_local_search(n, flow, dist, child_sol, child_cost, 10000, child_time)` method.

To change the architecture of the whole algorithm, you might want to modify the `FPBS_v1()` method.

## Citation
If you find the article or code useful for your project, please refer to
```
@Article{Zhou2022,
  author  = {Zhou, Yangming and Hao, Jin{-}Kao and Duval, Béatrice},
  journal = {{IEEE} Trans. Syst. Man Cybern. Syst.},
  title   = {Frequent Pattern-Based Search: A Case Study on the Quadratic Assignment Problem},
  year    = {2022},
  number  = {3},
  pages   = {1503-1515},
  volume  = {52},
}
```
## Paper
See the Paper folder
