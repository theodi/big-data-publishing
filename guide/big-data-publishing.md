# A Guide to Publishing Big (Open) Data

*Tom Heath, Ulrich Atz, et al.
*The Open Data Institute


## Executive Summary


## Introduction

The notion of *Big Data* has gained significant coverage in the technology press and broader media. It is sold to businesses as the next big thing. Most definitions of the term reference the three Vs (Volume, Variety, and Velocity) [ref] and loosely define Big Data as that which is not easily managed using traditional computing and data management approaches and infrastructures [ref]. Needless to say, 'traditional' remains ambiguous, and the volume of data that may be easily processed on any infrastructure continues to increase, making it almost impossible to quantify Big Data.

A more meaningful understanding of the concept may be gained by considering the context of deployment and usage. As a broad generalisation, the majority of the discourse on the topic centres around or assumes Big Data deployment and usage in the enterprise. For example, a large retailer may process massive volumes of transaction data to produce insights into shopping habits. This may be an exercise with purely internal data, e.g. which items are bought at the same time, or it may attempt to relate purchasing habits to external factors, e.g. weather or sporting events, that involve consumption of third party data which is likely smaller in volume.

In either case, data processing is assumed to take place behind the firewall, where it can be transferred across corporate networks or aggregated in a data warehouse. Less consideration is given to scenarios where data is published in the open for reuse by a wide range of consumers. In such cases, distribution of the data across the Internet presents the first challenge, before any processing can take place. The limitations of network connectivity available for accessing large data sets may mean that a more conservative quantification of Big Data is required when considering publication of 'Big Open Data'. For example, a data volume that may be trivial to transport on an internal network may be impractical to publish on the Web without taking special measures.

\[UA: Some comment on different users, e.g. non-technical audiences]

This guide is designed to highlight the challenges presented when openly publishing data via the Web (or through other Internet-based protocols) and, where possible, to highlight the measures that can be taken to mitigate these challenges. Crucially, these challenges do not relate simply to volume or velocity of the data published, but to technical, practical and legal factors that may hinder the utility/usability of the data if not addressed.


## Case Studies of Big Open Data Publication

We illustrate different ways of publishing data on the web with three current examples:

1. The first one, [1,000 Genomes](http://www.1000genomes.org/data#DataAccess), is an extreme case in terms of size. With 260 terabytes, and growing, it is one of the largest distributed data projects ever undertaken in biology. 
2. The [Tiny Images Dataset](http://horatio.cs.nyu.edu/mit/tiny/data/index.html), despite its size of hundreds of gigabytes, provides a simple download link, which is familiar to most web users.
3. The third example, [BioTorrents](http://www.biotorrents.net/), employs a more unconventional, distributed publication form and uses the BitTorrent protocol.

\[UA] Test

- [Case Study 1](#1000genomes)
- [Case Study 2](#tinyimg)
- [Case Study 3](#biotorrents)


### [1,000 Genomes](id:1000genomes)
#### Description

The 1,000 Genome project provides a resource on human genetic variation by sequencing the genomes of a large number of people. Details of the project are published in an [article in Nature Methods](The 1000 Genomes Project: data management and community access): "In March 2012 the still-growing project resources include more than 260 terabytes of data in more than 250,000 publicly accessible files." The Wellcome Trust alone supports the project with an amount above £5 million. 

Distributing the data poses several technical challenges:

###### 1. Discovering parts of the data
Some people do not want to or cannot download all of the data. We describe the main method for publication in the next section. The 1,000 Genomes project also provides key components of the data via Amazon Web Services as an alternative distribution channel. 

The authors notice that most users are more interested specific regions of the genome rather than the entire data set. Consequently, the files are distributed in directories named for the sequence. The complexity of the data, however, may make it extremely difficult to find the relevant parts. The publishers provide among other tools a **directory file**, a **FTP search tool** and a **data browser** to assist users in searching the data.


###### 2. Downloading the whole data

Some \[UA: all?] TCP based protocols such as FTP do not scale well. The 1,000 Genomes project relies on a service from [Aspera](http://asperasoft.com/): Their UDP-based method achieves data transfer rates which in typical usage are 20-30 times faster than FTP. Aspera's [fasp&trade;](http://asperasoft.com/technology/transport/fasp/) is a commercial product, but is, according to one technical team member, used with great success.

At least two mirror download sites provide access simultaneously and efficiently increase the overall download capacity.


#### In conclusion
The 1,000 Genome project tackles the technical challenges by publishing the data in different ways. 

Users can download the whole data set with a comparable, but faster version FTP. Parts of the data are available and discoverable via a FTP structure, a FTP search, a data slicer, the 1000 Genomes browser, a public Mysql Instance and a mirror in the Amazon Simple Storage Service (S3).

Additional support is manifold. Announcements are made available via RSS, Twitter and also via an email list. The website [1,000 Genomes](http://www.1000genomes.org) hosts all links and information about the data and the project. 


### [Tiny Images Dataset](id:tinyimg)
The Tiny Images data set consists of 79,302,017 images stored in the form of large binary files. They appear in an [academic paper](http://ieeexplore.ieee.org/xpl/login.jsp?tp=&arnumber=4531741&url=http%3A%2F%2Fieeexplore.ieee.org%2Fxpls%2Fabs_all.jsp%3Farnumber%3D4531741) on scene recognition from 2008.

In total there are 5 files that can be downloaded via a download link on the site:

  - Image binary (227 Gb)
  - Metadata binary (57 Gb)
  - Gist binary (114 Gb)
  - Index data (7 Mb)
  - Matlab Tiny Images toolbox (150 Kb) 

Publishing the data in such a way my be easy from a publisher's perspective but comes with a number of shortcomings: 

1. It is not possible to download parts of the data.
2. It seems, moreover, not possible to explore a sample of the data to see whether it suits a user's needs.
3. What happens if a user's internet connection is interrupted?
4. Support and documentation is very limited.




### [BioTorrents](id:biotorrents)



BioTorrent see three advantages compared to hosting files through FTP or HTTP:

* The BitTorrent protocol excels when the data is (very) large and multiple computers can seed (e.g. host) the data. Therefore, popular datasets that are often downloaded many times would see the largest benefit as bandwidth requirements are distributed across all computers seeding and actively downloading the data.
* BioTorrents can act as a central listing of results, datasets, and software that can be browsed and searched.
* Data can be located on several servers allowing decentralization and availability of the data if one server becomes disabled.

On the other hand, BioTorrents faces the problem that its requires users to download additional software to access torrents (files). Moreover, BitTorrent is often associated with illegale filesharing, which may become a barrier in some institutions. Lastly, a lot of technical questions remain open such as where to upload the torrent and how to communicate this method of publishing.

The BitTorrent protocol excels when the data is (very) large and multiple computers can seed (e.g. host) the data. Therefore, popular datasets that are often downloaded many times would see the largest benefit as bandwidth requirements are distributed across all computers seeding and actively downloading the data.



## Understanding Your Data

As the case studies above illustrate, there is great variety in the methods used for publication of Big Open Data. Before exploring the most appropriate methods for a particular data set it is critical to consider the nature of the data itself, and how this may influence the choice of publication mechanism.

\[*Use this as the lead into different sections on static vs streaming data (need to be clear on where the distinction lies, grey areas between the two etc); mention volume and velocity and how the two inter-relate*]

\[*question: how much of your data set will consumers actually want to use? How much **variety** do you have, will consumers typically want all of it? Example: a horizontal ecommerce site such as Amazon or Tesco.com; some consumers may want all of the core data (e.g. pricing), but others may only be interested in specific vertical segments.*]
	
\[*decision point: data dumps or some kind of API for more dynamic data (or both)*]


### Publishing Dumps of (Relatively) Static Data


#### Data Preparation and Distribution Protocols

##### Distribution Protocols

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

##### Hosting Programmes and Platforms

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


##### Sharding

\[for static dumps...sharding schemes, optimimum shard sizes for different platforms, impact of sharding schemes etc on processibility]


##### Compression

\[*Brief overview of the various lossless data compression schemes/agorithms; performance; splittability]

##### Importability

\[*Generic discussion/overview of different formats and how they impact on importability*]

\[*Discuss different consumption scenarios, e.g. public processing on EC2/EMR vs pulling down into a proprietary solution vs a behind the firewall solution on something like OpenStack]

\[*Object vs Block storage in e.g. Amazon EC2/EMR/S3; ease of mounting block storage from nodes in a cluster vs pulling down from object storage; compare this to disk requirements on each node; what is the optimum approach in different settings]


##### Costs



#### Metadata Publishing

##### licensing

##### provenance

##### referencing-and-linking

##### update frequency

#### collaboration

##### collaboration-over-data


### Publishing Dynamic Data

\[*clarify that much data is dynamic, but the importance of making this available in near real-time depends on how it will be used and what it will be used for, and practical issues such as scale*]

\[*e.g. high volume streaming data; lower volume but frequent updates; large data sets where consumers may only want a specific slice*]

\[*do all the same issues above apply, just in different ways?*]

\[*streaming APIs, regular HTTP APIs, your-website-is-your-api*]

\[*how to convey commit level (i.e. degree of 'consistency' of the data provided by a particular endpoint); e.g. an endpoint may be serviced by multiple servers with differing levels of consistency at any one time; how best to convey this to consumers? c.f. etags, headers indicating commit level...*]
