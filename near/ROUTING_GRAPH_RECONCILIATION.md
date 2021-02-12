# Overview
In P2P networks, like NEAR Protocol [1], each node stores a graph nodes and edges representing Peers and connections between them on the network.
We will call such graph a `routing graph`. Whenever a peer joins the network, or a connection gets lost and peers reconnect,
they exchange their routing tables. The process of exchanging tables involves adding edges, which are present in one's peers view of the graph, but not in the others. 
For the same of simplicity we will describe only the process of adding new edges.

That operation gets more expensive as `routing graph` grows larger. Exchanging full routing tables on every reconnect would be expensive and we would like to avoid it.

In this article, we will discuss ways of exchanging routing tables in a way that the amount of data send in proportional the number of edges that need to be inserted.

# Definitions
* Routing Graph - graph consisting of nodes and edges representing whole network
* Node

Each node is uniquely defined by it's PublicKey.
```rust
pub struct PeerId {
    /// Peer is defined by it's public key
    public_key: PublicKey,
}
```
* Edges

Each edge is defined by pair of peer ids and signatures of both peers. This data structure can be as large as 360 in case of NEAR Protocol network. Therefore we would like to minimize the number of edges we transfer.
```rust
pub struct Edge {
    /// Since edges are not directed `peer0 < peer1` should hold.
    pub peer0: PeerId,
    pub peer1: PeedId,
    /// Signature from parties validating the edge. These are signature of the added edge.
    signature0: Signature,
    signature1: Signature,
}

```
* IBF - Inverse Bloom Filter
`$A_b$`
`$D_A$`
  dsffsd
```latex D_A```
  
Invertible Bloom Filter (IBF) is a type of bloom filter, which can be used to simultaneously calculate `D_{A}−B` and DB−A using O(d) space. This
  data structure encodes sets in a fashion that is similar in spirit to
  Tornado codes’ construction [6], in that it randomly combines elements using the XOR function
Full definition of IBF can be found at `ESRwPC [4]`.

# Estimation algorithms

# Algorithm for Edges Reconciliation

# Vulnerabilities

# Results

# References
- [1] https://near.org/
- [2] Efficient Set Reconciliation without Prior Context. https://www.ics.uci.edu/~eppstein/pubs/EppGooUye-SIGCOMM-11.pdf
- [3] Minisketch: a library for BCH-based set reconciliation https://github.com/eupn/minisketch-rs
- [4] Efficient Set Reconciliation without Prior Context https://www.ics.uci.edu/~eppstein/pubs/EppGooUye-SIGCOMM-11.pdf
