# Purpose of these pages

In this Wiki I will try to describe my experience of deployment and configuring SolrCloud for Sitecore 9.0.1

# How does that SolrCloud look like?

My deployment was done into Virtual Machines in **Microsoft Azure**. VMs where organized in **Azure Virtual Network** and all the communications between SolrCoud nodes and Zookeeper nodes was done within that vNet.

# Used information sources
I didn't have experience with SolrCloud at all, therefore I searched a loot for the information. I found following articles useful:
* [solr-cloud-setup-with-zookeeper-for-sitecore](https://sitecorenuke.wordpress.com/2017/08/31/solr-cloud-setup-with-zookeeper-for-sitecore/)
* [setting-up-an-external-zookeeper-ensemble](https://lucene.apache.org/solr/guide/6_6/setting-up-an-external-zookeeper-ensemble.html)
* [securing-solr-cluster-enabling-ssl-on-multi-node](https://javadeveloperzone.com/solr/securing-solr-cluster-enabling-ssl-on-multi-node/)
* [Solr documentation enabling ssl](https://lucene.apache.org/solr/guide/6_6/enabling-ssl.html)
* [Solr documentation command line utiliries](https://lucene.apache.org/solr/guide/6_6/command-line-utilities.html)
* [Sitecore community: Install and configure SolrCloud](https://sitecore-community.github.io/docs/search/solr/Install-and-configure-SolrCloud/)

However, some of such articles contain confusing information which may lead to configuring SolrCloud incorrectly. 

# Resulting infrastructure

![sitecore solrcloud](/images/SolrCloud_infrastructure_http.jpg)

## Explanation

There are 3 Windows VMs with Windows Server 2016 Datacenter and Solr and Zookeper running on each as Windows service.
Actually, general best practice is to run Zookeeper instances on separate machines. In my case, it was decided to run them together on every single VM. 
