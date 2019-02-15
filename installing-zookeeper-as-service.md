# Installing Zookeeper as a Windows service

As I mentioned before, I used [NSSM](https://nssm.cc/) tool for running both Zookeeper as well as SolrNode as windows services.

## Download and un-archive Zookeeper

Zookeeper can be found [here](https://zookeeper.apache.org/releases.html). I used latest stable release `zookeeper-3.4.12`.

## Zookeeper Configuration

1. Create Zookeeper data folder. For example `c:\zk\data`
2. Rename `zoo_sample.cfg` file in Zookeeper folder to `zoo.cfg` (can be found in `Conf` folder of Zookeeper distribution)
3. Update `dataDir` setting in `zoo.cfg` to point to the folder created earlier: so it will look like `dataDir=C:/zk/data`
3. Add entries for your Zookeeper servers(nodes) into `zoo.cfg`.
   
   > **Note**: that should be IP Addresses if the VMs with SolrNodes nodes, not Zookeper ones (this is in case you have your Zookeeper nodes running on dedicated VMs)
   
   That will look like in following example. Please pay attention that since my VMs are in Azure vNet, it uses internal IP addresses there.
   
   ```
   server.1=10.1.0.9:2888:3888
   server.2=10.1.0.11:2888:3888
   server.3=10.1.0.10:2888:3888
   ```
   > **Note**: important to have such format of the configuration: server.<number> (there must be `.` (dot) between, otherwise SolrCloud setup won't work)

4. Now a bit magical step. In your Zookeeper data folder (defined in step #1, is `c:\zk\data` in my example) create file with name `myid` without extension and add there identificator of your Zookeeper node. The number after `.` (dot) from the step #3.
   So, in my example, for the server with IP `10.1.0.9` the contents of the `myid` file should be `1`, for the server `10.1.0.11` is `2` and so on.

5. Install and run Zookeeper as a Windows service. Use NSSM for that: start following command:

   `<path_to_nssm_distributive>\nssm.exe install`
   
   Configure service in the window appeared. Run `<path_to_zookeeper_root>\bin\zkServer.cmd` file. See an example how to install service by NSSM in this [example of running standalone Solr service](https://www.norconex.com/how-to-run-solr5-as-a-service-on-windows/). Basically it is similar process for ZooKeeper as well as for Solr node services to run them as Windows services using NSSM. The difference is just a matter of naming, executable and parameters that should be supplied to that executable. 

   Don't forget to start your service running following command in CMD:

   `net start <your_service_name>`

6. Finally, if SolrCloud should be running with SSL turned on, ZooKeeper should have a property `urlScheme` set to `https`. For that run following command (for the simplicity sake I left in the command below the path to the Solr distributive, you should of course change that to your one):

   ```
   c:\solr\solr-6.6.2\server\scripts\cloud-scripts\zkcli -zkhost "10.1.0.9:2181,10.1.0.10:2181,10.1.0.11:2181" -cmd clusterprop -name urlScheme -val https
   ```

7. Of course do steps above on all the VMs that you want to use as Zookeeper nodes
