- version 4.10.11:
    - A bug fixed where number of taxa = 64*X was throwing an error
    
- version 4.10.10:
	- Very significant improvement in the running time for datasets with many polytomies in input gene trees
	- Some running time improvement for datasets without polytomies 
	- A little bit of simplifying code refactoring
	 
- version 4.10.9:
	- A bug introduced in 4.10.8 is fixed. Version 4.10.8 simply did not run
	- Added `--gene-only` for gene-only bootstrapping
	 
- version 4.10.8:
	- Output taxon occupancy
	- Don't error out on gene trees with dummy degree 2 nodes
	- Check the species name against gene names for identity. 
	 
- version 4.10.7:
	- Small bug fix: with `-a` scoring using `-q` didn't work. Also, output both gene tree labels and the species tree labels. 
	- Bug fix: effective N and quartet scores were not correctly printed out with -t X options if gene trees had polytomies. posterior values were correctly computed.
	- Warning for low `EN` values.
	- Some spell checking on prompts
	
- version 4.10.6:
    - Small bug fix: with `-a` scoring didn't work
    - Print tree topology to stderr before scoring it. 
    - Warn for multi-individual datasets that this is not the right branch
    - Update tutorial

- version 4.10.5:
	- Hide `-y` option for now. Not ready for prime time yet. 
	
- version 4.10.4:
	- New option `-y` to score all possible trees; when used with `-t 12` outputs only the tree(s) with the best sum log local posterior
	- Change handling the scoring of root nodes
	- Add a bunch of for-test-only `-t` options
	 
- version 4.10.3:
	- *Important change:* change calculation of local PP for trees with missing data. Avoid up-weighting genes with fewer missing leaves. 
	- New feature: `-t 10` tests for polytomies. 
	
- version 4.10.2:
	- Bug fix: when in rome do as the americans do. For people using European machines, the support values were printed with a comma, wreaking havoc in the newick format. Has to use US format for those to fix this.


- version 4.10.1:
	- BUG FIX: Branch lengths could be negative in rare situations (few genes). This was because checks were for ML instead of MAP. 
	- Some extra stuff were outputted to the log. Removed. 
	- BUG FIX: For scoring a tree, the output was written to stdout instead of `-o`

- version 4.10.0:
	- Merge branch length and support calculation with the main branch
	- Update documentation.
	 
- version 4.9.9:
	- New Feature: ability to set lambda (the prior parameter) using `-c`
	- Some internal code refactoring
	 
- version 4.9.8:
	- BUG Fix: There was a small bug in branch length computation (akin to using wrong priors). This affected mostly long branches, where prior became important. Fixed the bug. 

- version 4.9.7:
	- BUG Fix: for very large n (>30000), posterior probability could under or overflow. Fixed the issue. 
	
- version 4.9.6
	- BUG Fix: 0.3 instead of 1/3 was used for branch length 
	
- version 4.9.5
	- BUG Fix: fix branch length again. For q<1/3, return 0. Also, return MAP instead of ML. 
	 
- version 4.9.4: 
	- BUG Fix: branch length for short branches should be using -ln(3p)
	 
- version 4.9.3:
	- Add `-t 4`
	 
- version 4.9.2:
	- first attempt at fixing numerical bugs for corner cases (not necessarily fixed)
	 
- version 4.9.1:
	- Improve handling of missing data for posterior calculation. Use effective n
	
- version 4.9.0:
	- Now compute posterior probabilities as will (calculations to be published)
	
- version 4.8.5:
	- Ignore species tree polytomies when scoring
	 
- version 4.8.4:
	- multifurcating input gene trees are accepted now. 
	 
- version 4.8.3:
	- use semicolon instead of `,` in branch length labels. Also output the total number of quartets around each branch in the species tree
	 
- version 4.8.2:
  - add options to control the amount of branch annotation
   
- version 4.8.1:
  - Major improvement: ASTRAL now computes branch lengths in coalescent units and also computes a quartet support for each branch 

- version 4.7.12:
  - Added an option (-c) so that ties are broken randomly

- version 4.7.8:
  - Fixed a bug in normalization of quartet scores. For very large datasets, the normalization of the quartet scores was incorrect. This only affected the outputted normalized score. 
    The tree topology, and the non-normalized scores were not affected. 

- version 4.7.7:
  - added a new option to filter genes by taxon occupancy

- version 4.7.6:
  - Made sure multi-allele works with new features added after 4.7.0 
  - Output normalized score with -q option

- Version 4.7.5:
  - Added an option to output the search space to standard output. (-k searchspace_norun) 	

- Version 4.7.4:
  - Adjust max polytomy size using sqrt of n
  - Misc refactoring and small bug fix (speed mostly)

- Version 4.7.3:
  - Resolving gene tree polytomies using a hybrid greedy/distance method
  - Adding to X by resolving polytomies using distances in addition to greedy
  - Changing -p1 and -p2 settings. -p2 is now much slower than -p1
  - Now -p1 is the default
  - Code refactoring
  - Some log changes
  - Removing the unnecessary global vertex cache (used up memory/time)
  
- Version 4.7.2:
  - Changed the way extra bipartitions are added for unresolved gene trees
  - Made some changes to the default strategy for addition of extra bipartitions (do not add incompatible bipartitions - these can increase running time drastically with little benefit)
  - Fixed a bug regarding addition of extra bipartitions using greedy (affects running time)
  - Change some logging statements. 
  - Some code refactoring
  
- Version 4.7.1:
  - Fixed bootstrapping to consume much less memory.
  - Do not cache weights. Consumes memory and there is barely any reuse.
  - New option to output completed gene trees
  - New option to just output bootstrap inputs and exit. 

- Version 4.7.0:
  - Changed how bipartitions from trees with missing data are completed. In new version, gene trees are completed based on a four point condition approach. 
  - Added a new mechanism based on greedy consensus for adding bipartitions to X
  - Added arbitrary resolutions of polytomies in input gene trees to set X
  - Optimization for scoring gene trees with polytomies (prune 0,0,0 sides)
  - Fixed to tree-based algorithm for score calculation (a bit slower for small and low ILS datasets)
  - Changed option p to have three values: 0 (no addition), 1 (addition by greedy), and 2 (addition by greedy and distance) 
  - Added option q to score a given species tree
  - Changed log messages a bit.
  - More code refactoring
  - Added normalized score
	 
- Version 4.6.3:
  - Fixed bug in calculation of the distance matrix for addition of extra bipartitions and completion of incomplete gene trees
  - Improved scalability of missing taxon completion algorithm (n^2 logn+n|X|^2)
  - Fixed numerical bugs related to very large number of taxa (e.g. 1000); `long` is now used everywhere
  - A bit of code refactoring
  - Adding more stderr logs
  - Added `-p` option to prevent addition of extra taxa
 
- Version 4.6.2:
  - Merge in 4.4.3 and 4.4.4 to multi-allele branch
  
- Version 4.6.1:
  - Merge in 4.4.2 changes to multi-allele branch
  
- Version 4.6.0:
  - Incorporate bug fix from 4.4.1
  
- Version 4.6.0:
  - Handle unresolved gene trees
    
- Version 4.5.1:
    - This version automatically adds extra bipartitions using a calculations based on quartet distances between two taxa 	

- Version 4.5.0:
  - ASTRAL can now handle multi individual gene trees

- Version 4.4.4:
  - Added a script to fix support values on output files that were incorrect from version 4.3.1 to 4.4.1

- Version 4.4.3:
  - Print bootstrap support as internal branch labels instead of branch length values
  - ** Bug fix**: on some machines greedy used to choke (see commit 807edf)
    
- Version 4.4.2:
  - **Bug Fix (IMPORTANT):** Support values drawn on the main tree were incorrect in previous versions since 4.3.1 (related to rerooting of trees). 
  - Prompts changed slightly 
 
- Version 4.4.1:
  - Print a user-friendly error when extra trees have taxa not in main trees.

- Version 4.4.0:
  - **Bug fix:** when gene trees had extreme levels of missing taxa, and there existed two taxa that never appeared together in the same gene tree, an uncaught division by zero could lead to wrong placement of one or both taxa. 
    
- Version 4.3.1:
  - Output consensus bootstrap tree as well
  - Output support only for internal branches
  - Fix default seed number to 692
  - Root all output trees *arbitrarily* on one taxon

- Version 4.3.0 (**command-line options changed!** Notice some commands are not backward compatible!):
  - Performs bootstrapping (`-b`, `-r`, `-g`, `-s` added)
  - Uses a library for argument parsing. We had to change some of the option names (exact version: `-xt` --> `-x`, extra trees: `-ex` --> `-e`).
  - Does not output the number of quartets satisfied by each branch; that information was not interpretable. 

- Version 4.2.1:
  - Read input gene trees with internal node labels
  - Updated the prompts and messages (e.g. Score instead of Cost)
  - Software outputs the version number too

- Version 4.2.0:
  - **Bug fix:** overflow happened for large number of genes.  Use long instead of int
  - Improve the command-line help a bit

- Version 4.1.1:
  - Added a hidden option to force algorithm used for estimation (only for debugging) 

- Version 4.1:
  - Updated the command-line so that ASTRAL algorithm is the default and DynaDup specific options are removed (-wq omitted and is default now)

- Version 4.0:
  - Added support for handling missing data by completing bipartitions
