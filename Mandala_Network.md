
**Mandala networks** refer to a family of networks which are fast, cost-effective, and robust against [[Failures|failures]] and [[Attacks|attacks]]. They are built up in layers (often called *shells* or *generations*) and derive their name from a visual similarity to mandala images. These networks are defined by a mathematical construction presented in [[Mandala_Networks_Reference|[1]]].

---

## Defining Characteristics

Mandala networks exhibit:

- **Ultra-small-world** properties  
- **High sparsity**  

By design, these attributes reduce average path lengths between nodes while keeping overall network connectivity efficient.

---

## Construction Parameters

In their basic form, **Mandala networks** are characterized by three parameters:

$$
(s,\, b,\, \lambda)
$$

where:

- \( s \) is the number of nodes in the first generation (or shell).  
- \( b \) is the number of new nodes added for *each node* in subsequent shells.  
- \( \lambda \) is the number of *intra-shell* connections (excluding the first shell).

A unique Mandala network is defined by the type \((s, b, \lambda)\) and the total number of shells, which we may denote as \( n \).


---

### Iterative Shell Construction

1. **First Shell**  
   - Contains \(s\) nodes forming a connected graph.

2. **Second Shell**  
   - Each node in the first shell spawns \(b\) new nodes in the second shell.
   - Each new node in the second shell is connected to \(\lambda\) other nodes within the second shell itself.

3. **Third Shell**  
   - Constructed similarly by adding \(b\) new nodes per node from the shell above.
   - Each node in the third shell connects to its ancestor in the first shell as well, ensuring a maximum shortest path length of 3 between any two nodes in the network.

This process repeats iteratively up to \(n\) shells. Because every node in higher shells links directly back to a node in the first shell (which is also directly connected to other nodes in the first shell), the maximum shortest path length across the entire network remains 3.

---

## Number of Nodes

Let \( N_i \) denote the number of nodes in the \( i \)-th shell. Then, the **total number of nodes** in the network up to \( n \) shells can be written as:

$$
\sum_{i=1}^n N_i
$$

---

## Mean Shortest Path

Due to the construction’s symmetry, the **mean shortest path length** \( \phi_n \) for a node in the \( k \)-th shell (and all nodes in the network) can be expressed using a function of:

$$
\phi_n = \frac{1}{N} \sum_{\text{all nodes}} d\bigl(\text{node}, k\text{-shell nodes}\bigr)
$$

where \( N \) is the total number of nodes, and \( d(x,y) \) denotes the shortest path distance between nodes \( x \) and \( y \). It can be shown that \( \phi_n \) grows very slowly (logarithmically or slower) as \( n \to \infty \), confirming the **ultra-small-world** characteristic.

---

## References

- **[1]** [*Mandala Networks: ultra-small-world and highly sparse graphs* (Sampaio Filho, C., Moreira, A., Andrade, R. et al. Sci Rep 5, 9082 (2015))](https://www.nature.com/articles/srep09082)  
  DOI: [10.1038/srep09082](https://doi.org/10.1038/srep09082)

---

## Tags
- [[Mandala_Networks]]
- [[Ultra_Small_World]]
- [[Sparse_Graphs]]
- [[Network_Topology]]
- [[Graph_Theory]]
- [[Connectivity]]
- [[Scalability]]
- [[Shells_Generations]]
- [[Shortest_Path]]
- [[Failures]]
- [[Attacks]]
