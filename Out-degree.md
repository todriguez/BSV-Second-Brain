```markdown
---
title: Out-degree
---

# CAUTION: AI GENERATED CONTENT | NEEDS REVIEW

## Definition

The out-degree of a node in a directed graph is the number of edges leaving from it. In other words, it signifies the number of direct successors a node has in a graph. 

Note that this concept applies only to [[Directed Graphs]], as only these types of graphs have clear differentiation between inbound and outbound edges.

## Calculation

The out-degree of a node can be calculated by counting the number of arrows (edges) leaving from it. The calculation does not include edges coming into the node (in-degree).

An example would be if we have a node **A** which has three arrows to other nodes **B**, **C** and **D** respectively. The out-degree of node **A** is 3.

## Use Cases

Out-degree is often used in network analysis within the field of [[Network Theory]], to understand the properties of a particular node. It can give insights such as how a node might influence others in a network.

For instance, in social network analysis, a node with a high out-degree may be interpreted as a highly influential person who affects a great number of people in the network. In this context, out-degree is also seen as a measure of centrality: the more edges a node has going out, the more central the node is, and therefore potentially more important or influential.

## Example

Think of your favorite social media platform such as Twitter. If you post a status update (thus creating edges to your followers), your 'out-degree' would be the count of your followers provided that the edges aren't reciprocated. Thus, if you have 100 followers and you post an update, your out-degree over that time is 100.

Keep in mind that analyzing out-degree alone might not represent the full story of a node's influence or importance. It's often analyzed in conjunction with other metrics such as [[In-degree]], [[Degree Centrality]] or [[Closeness Centrality]].
```