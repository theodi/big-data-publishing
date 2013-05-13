# A Guide to Publishing Big Data

*Tom Heath, Ulrich Atz, et al.
*The Open Data Institute

## Introduction
\[*Some intro text here...*]


## Case Studies of Big Data Publication

* Amazon Public Datasets Programme
* COINS data
* DBpedia?


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
    * ...

##### Hosting Programmes and Platforms

* Hosting Programmes
    * Amazon Public Data Sets
    * Google equivalent?

* Hosting Platforms
    * OpenStack Storage <http://www.openstack.org/software/openstack-storage/>
    * Riak Cloud Storage <http://basho.com/riak-cloud-storage/>

* Hosting Services
    * Amazon S3
    * Rackspace Cloud
    * *others...*


##### Sharding

\[sharding schemes, optimimum shard sizes for different platforms, impact of sharding schemes etc on processibility]

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

