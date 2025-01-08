getblocktemplate is a now deprecated protocol used to transmit block
template information from nodes to remote hash machines. It was
developed in 2012 and superseded the original \"getwork\" protocol.

# Reasons for development

The original getwork protocol only provided ASIC Miners with a single
block header, which was sufficient for a total of 4 GH of mining. With
the \"rollntime\" extension, this was extended to 4 GH \*per second\*,
but even that was far from sufficient for mining equipment at the time
which was already capable of 1000 GH/s on the high end.

# Attribution

This content is based on content sourced from
[https://en.bitcoin.it/wiki/Getblocktemplate](https://en.bitcoin.it/wiki/Getblocktemplate)under [Creative Commons Attribution 3.0](https://creativecommons.org/licenses/by/3.0/). Although it may have been extensively revised and
updated, we acknowledge the original authors.