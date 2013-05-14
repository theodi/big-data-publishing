# A Guide to Publishing Big Data

*Tom Heath, Ulrich Atz, et al.
*The Open Data Institute


## Executive Summary


## Introduction

The notion of *Big Data* has gained significant coverage in the technology press and broader media. Most definitions of the term reference the three Vs (Volume, Variety, and Velocity) [ref] and loosely define Big Data as that which is not easily managed using traditional computing and data management approaches and infrastructures [ref]. Needless to say, 'traditional' remains ambiguous and the volume of data that may be easily processed on any infrastructure continues to increase, making it almost impossible to quantify Big Data.

A more meaningful understanding of the concept may be gained by considering the context of deployment and usage. As a broad generalisation, the majority of the discourse on the topic centres around or assumes Big Data deployment and usage in the enterprise. For example, a large retailer may process massive volumes of transaction data to produce insights into shopping habits. This may be an exercise with purely internal data, e.g. which items are bought together, or it may attempt to relate purchasing habits to external factors, e.g. weather or sporting events, that involve consumption of third party data.
[... either way the big data is behind the firewall]


\[*Some intro text here...*]

\[*What do we mean by Big Data? Brief nod to the typical definitions (e.g. 3Vs), but then move on to practical considerations. Emphasise that it's a sliding scale and that the **publication** issues start presenting themselves at an early stage, e.g. as low as 10s or 100s of GB. Contrast big data behind the firewall (where the publication problems may not exist, it may simply be a case of large internal databases) with open publication of large data sets*]



## Case Studies of Big Open Data Publication

* Amazon Public Datasets Programme
* COINS data
* DBpedia?
* Common Crawl?
* Weather data?
* LHC???


### What form does your data take?

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
    * Amazon Public Data Sets
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
