#<p>puppet-master-2slaves</p>

<p><i> Vagrant mans and scripts for setting up the puppet master-2slaves environment</i></p>
<p><i>Vagrant Multiple-VM Creation and Configuration</i></p>

<p><i>Automatically provision multiple VMs with Vagrant and VirtualBox. Automatically install, configure, and test Puppet Master and Puppet Agents on those VMs. All instructions can be found in my blog post: http://wp.me/p1RD28-1kX</i></p>

<p><i>JSON Configuration File</i></p>

<p><i>The Vagrantfile retrieves multiple VM configurations from a separate nodes.json file. All VM configuration is contained in the JSON file. You can add additional VMs to the JSON file, following the existing pattern. The Vagrantfile will loop through all nodes (VMs) in the nodes.json file and create the VMs. You can easily swap configuration files for alternate environments since the Vagrantfile is designed to be generic and portable.</i></p>

<p><i>Instructions</i></p>

<p>`vagrant up` # brings up all VMs</p>
<p>`vagrant ssh puppet.example.com`</p>

<p>`sudo service puppetmaster status` # test that puppet master was installed</p>
<p>`sudo service puppetmaster stop`</p>
<p>`sudo puppet master --verbose --no-daemonize`</p>
<p># Ctrl+C to kill puppet master</p>
<p>`sudo service puppetmaster start`</p>
<p>`sudo puppet cert list --all` # check for 'puppet' cert</p>

<p># Shift+Ctrl+T # new tab on host</p>
<p>`vagrant ssh node01.example.com` # ssh into agent node</p>
<p>`sudo service puppet status` # test that agent was installed</p>
<p>`sudo puppet agent --test --waitforcert=60` # initiate certificate signing request (CSR)</p>

<p><i>Back on the Puppet Master server (puppet.example.com)</i></p>

<p>`sudo puppet cert list` # should see 'node01.example.com' cert waiting for signature</p>
<p>`sudo puppet cert sign --all` # sign the agent node(s) cert(s)</p>
<p>`sudo puppet cert list --all` # check for signed cert(s)</p>
<p><i>Forwarding Ports</i></p>

<p><i>Used by Vagrant and VirtualBox. To create additional forwarding ports, add them to the 'ports' array. For example:</i></p>

<p> "ports": [</p>
<p>        {
<p>          ":host": 1234,</p>
<p>          ":guest": 2234,</p>
<p>          ":id": "port-1"</p>
<p>        },</p>
<p>        {</p>
<p>          ":host": 5678,</p>
<p>          ":guest": 6789,</p>
<p>          ":id": "port-2"</p>
<p>        }</p>
<p>      ]</p>

<p><i>Useful Multi-VM Commands</i></p>

<p><i>The use of the specific name is optional.</i></p>

<p>`vagrant up` <machine></p>
<p>`vagrant reload` <machine></p>
<p>`vagrant destroy -f <machine> && vagrant up <machine>`</p>
<p>`vagrant status <machine>`</p>
<p>`vagrant ssh <machine>`</p>
<p>`vagrant global-status`</p>
<p>`facter`</p>
<p>`sudo tail -50 /var/log/syslog`</p>
<p>`sudo tail -50 /var/log/puppet/masterhttp.log`</p>
<p>`tail -50 ~/VirtualBox\ VMs/postblog//Logs/VBox.log`</p>
