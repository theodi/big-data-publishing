# A Guide to Publishing Big (Open) Data

*Tom Heath, Ulrich Atz, et al.
*The Open Data Institute


## Executive Summary


## Introduction

The notion of *Big Data* has gained significant coverage in the technology press and broader media. Most definitions of the term reference the three Vs (Volume, Variety, and Velocity) [ref] and loosely define Big Data as that which is not easily managed using traditional computing and data management approaches and infrastructures [ref]. Needless to say, 'traditional' remains ambiguous, and the volume of data that may be easily processed on any infrastructure continues to increase, making it almost impossible to quantify Big Data.

A more meaningful understanding of the concept may be gained by considering the context of deployment and usage. As a broad generalisation, the majority of the discourse on the topic centres around or assumes Big Data deployment and usage in the enterprise. For example, a large retailer may process massive volumes of transaction data to produce insights into shopping habits. This may be an exercise with purely internal data, e.g. which items are bought at the same time, or it may attempt to relate purchasing habits to external factors, e.g. weather or sporting events, that involve consumption of third party data which is likely smaller in volume.

In either case, data processing is assumed to take place behind the firewall, where it can be transferred across corporate networks or aggregated in a data warehouse. Less consideration is given to scenarios where data is published in the open for reuse by a wide range of consumers. In such cases, distribution of the data across the Internet presents the first challenge, before any processing can take place. The limitations of network connectivity available for accessing large data sets may mean that a more conservative quantification of Big Data is required when considering publication of 'Big Open Data'. For example, a data volume that may be trivial to transport on an internal network may be impractical to publish on the Web without taking special measures.

This guide is designed to highlight the challenges presented when openly publishing data via the Web (or through other Internet-based protocols) and, where possible, to highlight the measures that can be taken to mitigate these challenges. Crucially, these challenges do not relate simply to volume or velocity of the data published, but to technical, practical and legal factors that may hinder the utility/usability of the data if not addressed.


## Case Studies of Big Open Data Publication

This section presents three case studies of open publication of big data, covering a range of data volumes and publication methods...

\[UA: I find this sectin very important - we should select perhaps 3 cases, which offer something that we can describe.]

* Amazon Public Datasets Programme
* COINS data
* DBpedia?
* Common Crawl?
* Weather data?
* LHC???

* [1000 Genomes data](http://www.1000genomes.org/data#DataAccess) with more than 260 TB. Some sort of FTP hierarchy
* 80 TB of archived [web crawl data](http://blog.archive.org/2012/10/26/80-terabytes-of-archived-web-crawl-data-available-for-research) available on request
* [Tiny Images Dataset](http://horatio.cs.nyu.edu/mit/tiny/data/index.html) simple download link. "Requirements: 300 GB diskspace"
* This looks very promising as a [Bittorrent case study](http://www.biotorrents.net/). More info here: <http://www.ncbi.nlm.nih.gov/pmc/articles/PMC2854681/>

\[More stuff here http://www.quora.com/Data/Where-can-I-find-large-datasets-open-to-the-public]


## Understanding Your Data

As the case studies above illustrate, there is great variety in the methods used for publication of Big Open Data. Before exploring the most appropriate methods for a particular data set it is critical to consider the nature of the data itself, and how this may influence the choice of publication mechanism.

\[*Use this as the lead into different sections on static vs streaming data (need to be clear on where the distinction lies, grey areas between the two etc); mention volume and velocity and how the two inter-relate*]

\[*question: how much of your data set will consumers actually want to use? How much **variety** do you have, will consumers typically want all of it? Example: a horizontal ecommerce site such as Amazon or Tesco.com; some consumers may want all of the core data (e.g. pricing), but others may only be interested in specific vertical segments.*]
	
\[*decision point: data dumps or some kind of API for more dynamic data (or both); which would you use when and why? comes back to the question of how much/what proportion of the data your consumers would want and how frequently it changes*]


## Publishing Dumps of (Relatively) Static Data


### Data Preparation and Distribution Protocols

#### File Formats

\[*CSV vs JSON vs XML vs RDFx vs proprietary db dumps vs whatever...*]


#### Distribution Protocols

* HTTP
    * Tools
        * e.g. talk here about things like wget that are nicer than a browser
    * Factors to consider:
        * Resumability
        * Throttling
* FTP
    * Advantages over HTTP?
* Bittorrent
    * From James: *We discussed distributing data over bittorrent, and how you can ensure provenance, reliability etc. Well, if you had the .torrent file contained in a data package type git repository and included an md5sum of the contents, you presumably could use that to verify that the torrented version was correct with the official release. Perhaps data packages (or other metadata formats) could be extended to include a md5sum of the data in the referenced file.*

#### Hosting Programmes and Platforms

* Hosting Programmes
    * [Amazon Public Data Sets](http://aws.amazon.com/publicdatasets)
    * Google equivalent?

* Storage/Hosting Platforms
    * OpenStack Storage <http://www.openstack.org/software/openstack-storage/>
    * Riak Cloud Storage <http://basho.com/riak-cloud-storage/> (has an S3 compatible API, apparently)

* Hosting Services
    * Amazon S3
    * Rackspace Cloud
    * *others...*


#### Partitioning/Sharding

For publication as static dumps, data sets beyond a certain size will likely need to be split up into smaller pieces to aid discovery, distribution, and reuse. This process could be referred to as *partitioning* or *sharding*, with different segments of one logical dataset contained within different files. Various (and multiple) partitioning schemes could be used for the same data set, depending on how the data may be used.

##### Logical Partitioning

Perhaps the most obvious partitioning scheme is to split the data into logical groups, according to how consumers may wish to use it. For example, descriptive product data may be partitioned by product category, while transaction or event data may be partitioned by time period (e.g. daily, weekly, monthly, yearly depending on the data volume).

##### Size-Optimised Partitioning

How the data will be retrieved and processed has an impact on how large each partition should be. On the one hand, a large number of small files published on the Web is desirable, as this enables each partition to be identified by its own URI at a granular level, referenced in other data sources and documents, and easily inspected with common desktop tools (e.g. spreadsheet applications or text editors).

On the other hand, a smaller number of larger files may have advantages for consumers of the data. For example, retrieving many small files over HTTP may incur a cumulative *round-trip time* that significantly and negatively impacts the time taken to download the entire data set.
\[*need to sanity check this with a networking expert*]

\[*any considerations here in ease of downloading? depends on tools being used*]

How the data may be processed downstream also has a bearing on the optimum file size of partitions. For example, *[Apache Hadoop](http://hadoop.apache.org/) MapReduce* is a widely used framework for large-scale, distributed data processing. Architectural features of the MapReduce framework and underlying HDFS filesystem dictate that storing and processing large numbers of small files is significantly less efficient and less reliable than processing fewer, larger files. These issues are described in more detail in the following articles:

* <http://blog.cloudera.com/blog/2009/02/the-small-files-problem/>
* <http://developer.yahoo.com/blogs/hadoop/apache-hadoop-best-practices-anti-patterns-465.html>

In conclusion, a sensible compromise may be to partition the data into multiple smaller files but publish these alongside larger files that combine many smaller partitions (i.e. using less fine-grained partitioning). Alternatively, larger files may be published alongside sample data so potential consumers can easily inspect the contents.


##### Processing-Optimised Sharding

\[*revisit default hash partitioner in hadoop; any benefits in particular sharding schemes that may avoid overloading certain nodes if the data is lumpy? is this getting too specific? is it actually possible to anticipate this and provide any general guidance?*]


#### Compression

\[*Brief overview of the various lossless data compression schemes/agorithms; performance; splittability]


#### Headers

\[*other HTTP headers that should be used/sent with the data?*]
\[*should also cover content types*]

#### Importability

\[*Generic discussion/overview of different formats and how they impact on importability*]

\[*Discuss different consumption scenarios, e.g. public processing on EC2/EMR vs pulling down into a proprietary solution vs a behind the firewall solution on something like OpenStack]

\[*Object vs Block storage in e.g. Amazon EC2/EMR/S3; ease of mounting block storage from nodes in a cluster vs pulling down from object storage; compare this to disk requirements on each node; what is the optimum approach in different settings]


#### Costs



### Metadata Publishing

#### licensing

#### provenance

#### referencing-and-linking

#### update frequency

### collaboration

#### collaboration-over-data


## Publishing Dynamic Data

\[*clarify that much data is dynamic, but the importance of making this available in near real-time depends on how it will be used and what it will be used for, and practical issues such as scale*]

\[*e.g. high volume streaming data; lower volume but frequent updates; large data sets where consumers may only want a specific slice*]

\[*do all the same issues above apply, just in different ways?*]

\[*streaming APIs, regular HTTP APIs, your-website-is-your-api*]

\[*how to convey commit level (i.e. degree of 'consistency' of the data provided by a particular endpoint); e.g. an endpoint may be serviced by multiple servers with differing levels of consistency at any one time; how best to convey this to consumers? c.f. etags, headers indicating commit level...*]
