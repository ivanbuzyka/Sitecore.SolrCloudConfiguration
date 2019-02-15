# Prerequisites for SolrCloud Node + Zookeeper Node VM

As I mentioned on the Home page, it was decided to go _"not really best practice"_ way and deploy Zookeeper Nodes on the same Server with SolrCloud nodes.

I used Windows Server 2016 Datacenter image from Azure Marketplace as a base for my VMs. 

Both things are running as Windows Services powered by [NSSM](https://nssm.cc/).

## What needs to be on the VM

On each VM should be JRE 1.8 installed.
> **Note**: I experience some issues when using JRE 10 for running Solr, so that I decided to go strictly with JRE 1.8
#

Make sure that Java is properly registered in Environment Variables:

![sitecore solrcloud java](/images/java_variables.png)

To check that, you may open command prompt and try to run following command. If it works, your Java is installed correctly.

`java -version`

![sitecore solrcloud java](/images/java-running.png)

Finally make sure Windows firewall on this VM allows inbound connections for some specific SolrCloud ports. See more information in [Ports and Firewalls](ports-and-firewalls-etc) article in this wiki.
