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

If the data to be published changes rarely, or the intention is to publish static, periodic snapshots of the data, then the data dump techniques described in the section below on *Publishing Data Dumps* will be most suitable. Conversely, if the data to be published has great *variety* or *velocity*, changes regularly, or is required by consumers in near real-time, the *Publishing Many Small Data Fragments* and *Publishing Streaming Data* section below will likely be of greatest value.


## Publishing Many Small Data Fragments

\[*question: how much of your data set will consumers actually want to use? How much **variety** do you have, will consumers typically want all of it? Example: a horizontal ecommerce site such as Amazon or Tesco.com; some consumers may want all of the core data (e.g. pricing), but others may only be interested in specific vertical segments.*]

\[*decision point: data dumps or some kind of API for more dynamic data (or both); which would you use when and why? comes back to the question of how much/what proportion of the data your consumers would want and how frequently it changes*]


### APIs and Web sites

\[*e.g. high volume streaming data; lower volume but frequent updates; large data sets where consumers may only want a specific slice; regular HTTP APIs, your-website-is-your-api, smaller chunks of data*]

\[*how to convey commit level (i.e. degree of 'consistency' of the data provided by a particular endpoint); e.g. an endpoint may be serviced by multiple servers with differing levels of consistency at any one time; how best to convey this to consumers? c.f. etags, headers indicating commit level...*]

### File Formats

\[*CSV vs JSON vs XML vs RDFx vs proprietary db dumps vs whatever...*]



## Publishing Data Dumps


### Compression

In many big data publishing scenarios it is highly desirable to compress the data before publication to reduce the size of files downloaded by consumers. Compression becomes particularly important as the volume of data increases, but does bring a number of disadvantages. For example, consumers must decompress files in order to inspect the data, and compressed files are less likely to be indexed by search engines, thereby limiting the discoverability of data and the potential for onward linking to related data. The remainder of the section briefly reviews various open compression formats that may be used for big data publishing.

Two formats that are widely supported are *Zip* and *Gzip*. \[*do both use the same compression algorithm?*]. The trade-offs between these two formats are discussed in more detail in [this article](http://www.differencebetween.net/technology/difference-between-zip-and-gzip/), but in this context the salient differences between these formats can be summarised as follows:

#### Support for Archives

The Zip format is able to gather together multiple input files into one output archive, compressing each input file individually. By contrast, Gzip is a pure compression format that relies on an external programme such as *Tar* to first collect multiple input files into one archive before compression.

#### Compression Performance

By compressing each file in an archive individually, Zip is unable to exploit redundancy between files in the archive, and therefore typically achieves inferior compression performance compared to Gzip. This performance difference can be significant, but is naturally dependent on there being more than one file in an archive [check this -- do they use the same compression algorithm?] and on the degree of redundancy between files in the archive.

\[*show some indicative stats about the performance of different methods on the same data in one file or split across several*]

#### Individual Files

Conversely, Zip has an advantage when individual files need to be retrieved from an archive, as each can be extracted without requiring the entire contents to be decompressed. In the case of Gzip applied to Tar archives, the Tar programme has a compression-aware mode that can extract specific files from an archive, but in the worst case the entire archive may need to be decompressed before the target file is located \[*double check that this is the case*]. It should be noted that the compression-aware mode in Tar supports multiple compression formats in addition to Gzip, including *Bzip2* and *LZO*.

#### Platform Support

Historically, use of the Zip format has been more prevalent on Windows platforms, while Gzip has a stronger association with Unix-like platforms (e.g. Mac OSX and Linux). In reality, all of these platforms support both compression formats, but users of each may be more familiar with the respective *de facto* standard for their platform and have tools more readily available. As a broad generalisation, consumers of big data are more likely to use Unix-like platforms, and therefore Gzip may be a sensible default, but the downstream usage context should always be considered.

[*Is Zip supported at all by Hadoop?*]

\[*splittability]
\[*BZ2, LZO?, 7Z(arch)?*]

In summary, the most appropriate compression scheme to adopt will depend on the intended audience, the tooling likely to be used, the nature of the data itself (i.e. it's inherent redundancy), and how it is packaged/partitioned for publication.


### Partitioning/Sharding

For publication as static dumps, data sets beyond a certain size will likely need to be split up into smaller pieces to aid discovery, distribution, and reuse. This process could be referred to as *partitioning* or *sharding*, with different segments of one logical dataset contained within different files. Various (and multiple) partitioning schemes could be used for the same data set, depending on how the data may be used.

#### Logical Partitioning

Perhaps the most obvious partitioning scheme is to split the data into logical groups, according to how consumers may wish to use it. For example, descriptive product data may be partitioned by product category, while transaction or event data may be partitioned by time period (e.g. daily, weekly, monthly, yearly depending on the data volume).

#### Size-Optimised Partitioning

How the data will be retrieved and processed has an impact on how large each partition should be. On the one hand, a large number of small files published on the Web is desirable, as this enables each partition to be identified by its own URI at a granular level, referenced in other data sources and documents, and easily inspected with common desktop tools (e.g. spreadsheet applications or text editors).

On the other hand, a smaller number of larger files may have advantages for consumers of the data. For example, retrieving many small files over HTTP may incur a cumulative *round-trip time* that significantly and negatively impacts the time taken to download the entire data set.

\[*any considerations here in ease of downloading? depends on tools being used*]

How the data may be processed downstream also has a bearing on the optimum file size of partitions. For example, *[Apache Hadoop](http://hadoop.apache.org/) MapReduce* is a widely used framework for large-scale, distributed data processing. Architectural features of the MapReduce framework and underlying HDFS filesystem dictate that storing and processing large numbers of small files is significantly less efficient and less reliable than processing fewer, larger files. These issues are described in more detail in the following articles:

* [The Small Files Problem][WhiteHadoopSmallFiles]
* [Apache Hadoop: Best Practices and Anti-Patterns][YahooHadoopAntiPatterns]

In conclusion, a sensible compromise may be to partition the data into multiple smaller files but publish these alongside larger files that combine many smaller partitions (i.e. using less fine-grained partitioning). Alternatively, larger files may be published alongside sample data so potential consumers can easily inspect the contents.


#### Processing-Optimised Sharding

\[*revisit default hash partitioner in hadoop; any benefits in particular sharding schemes that may avoid overloading certain nodes if the data is lumpy? is this getting too specific? is it actually possible to anticipate this and provide any general guidance?*]



### Distribution Protocols

* HTTP
    * Tools
        * e.g. talk here about things like wget that are nicer than a browser
    * Factors to consider:
        * Resumability
        * Throttling
* FTP
    * Advantages over HTTP?
* Rsync
* Bittorrent
    * From James: *We discussed distributing data over bittorrent, and how you can ensure provenance, reliability etc. Well, if you had the .torrent file contained in a data package type git repository and included an md5sum of the contents, you presumably could use that to verify that the torrented version was correct with the official release. Perhaps data packages (or other metadata formats) could be extended to include a md5sum of the data in the referenced file.*

### Hosting Programmes and Platforms

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



### Headers

\[*other HTTP headers that should be used/sent with the data?*]
\[*should also cover content types*]

### Importability

\[*Generic discussion/overview of different formats and how they impact on importability*]

\[*Discuss different consumption scenarios, e.g. public processing on EC2/EMR vs pulling down into a proprietary solution vs a behind the firewall solution on something like OpenStack]

\[*Object vs Block storage in e.g. Amazon EC2/EMR/S3; ease of mounting block storage from nodes in a cluster vs pulling down from object storage; compare this to disk requirements on each node; what is the optimum approach in different settings]


### Costs




## Publishing Streaming Data

\[*clarify that much data is dynamic, but the importance of making this available in near real-time depends on how it will be used and what it will be used for, and practical issues such as scale*]

\[*streaming APIs*]

\[*do all the same issues above apply, just in different ways?*]


## Metadata Publishing

### licensing

### provenance

### referencing-and-linking

### update frequency

## Collaboration

### collaboration-over-data

\[*need to remind ourselves what we want to say here*]


## Acknowledgements

\[*acknowledge people here who have helped*]


## References

[WhiteHadoopSmallFiles]:		http://blog.cloudera.com/blog/2009/02/the-small-files-problem/	"The Small Files Problem"
[YahooHadoopAntiPatterns]:	http://developer.yahoo.com/blogs/hadoop/apache-hadoop-best-practices-anti-patterns-465.html	"Apache Hadoop: Best Practices and Anti-Patterns"
