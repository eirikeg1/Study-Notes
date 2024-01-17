# #TODO FIX IMAGES!!!!


- In vector space classification, training set corresponds to a labeled set of points (equivalently, vectors)
- **Premise 1:** Documents in the same class form a contiguous region of space
- **Premise 2:** Documents from different classes don’t overlap (much)
- Learning a classifier: build surfaces to delineate classes in the space

# Centroids

# Rocchio classification

- Forms centroid/prototype per class
- Classification: nearest centroid
- Does not guarantee that classifications are consistent with the given training data

## K Nearest Neighbour (kNN)

- Define k-neighborhood as the k nearest neighbors of d
- Pick the majority class label in the neighborhood of training set
- Does not _train_ as it is simply matching based on labeled training set, but the _learning_ is by storing the labeled training examples
- **contiguity hypothesis**: it assumes that dataset fits well
- Finds non linear decision boundaries
- Scales well with bigger datasets
# Approximate nearest neighbour

---

## Different lookup strategies

- Brute force
- Tree-based algorithms
- Locality-sensitive hashing
- Quantization
- Graph-based algorithms

# Selecting your algorithm:

- A lot of different factors to consider
  - Dataset noise, size, clusters etc.
- Often a combination of multiple classifiers
- 
# Bias vs. capacity - notions/terms

- Too much **capacity**, low **bias**: memorizes, always says no to unseen data
- Not enough **capacity**, high **bias**: generalizes too much, classifies object as tree as long as it has something green in it
- **Capacity** (Variance): Ability to adapt to noise
- Important to have a good **Bias/Variance tradeoff**: usually almost the same of both
- Classifiers:
  - kNN has high variance and low bias.
  - NB has low variance and high bias.
    - Linear decision surface (hyperplane – see later)

# Voronoi diagrams

- Highlights regions and finds out what is the nearest neighbor based on regions on search
- ![[Pasted image 20231124165131.png | 350]]

# (Approximate) kNN Algorithms

---

## Brute Force

- Do full scan and get exact results
- Optimized implementations make heavy use of SIMD and GPUs
- Can be feasible but expensive

-[%%](<![[Pasted image 20231011112314.png | 800>)

## Tree-Based Algorithms

- Indexing:
  - Construct a tree by (randomly, even) partitioning the data
  - Construct a forest of trees
- Querying:
  - Start at query point
  - Select one or more trees, follow branches
  - Consider the points located in the regions you end up
- 
-[%%](<Pasted image 20231011112602.png | 700]]>)

## Locality-Sensitive Hashing

- Indexing:
  - Apply multiple hash functions h to each point to bucket them
  - Distance $d(x, y)$ is small → $Pr(h(x) = h(y))$ is high
- Querying:
  - Apply hashes to query point
  - Consider points in the buckets we hash to

## Quantization

- Recode the vectors to reduce the size of the dataset
- Replace each vector with a leaner, approximate and quantized representation
- Can be combined with an inverted index
## Graph-Based Methods

_Example: **Hierarchical Navigable Small World Graphs**_

- Similar concept to 6 handshake rule, there is usually very few steps from any node $a$ to any other node $b$
- Construct graph hierarchically
- Works pretty well for real-world data

