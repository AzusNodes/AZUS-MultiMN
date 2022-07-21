# Multiple MasterNode

A script which is easily create Multiple Masternodes of the same coin in the same VPS.

First of all you have to start one masternode using <a href="https://github.com/AzusNodes/AZUS-MNScript/blob/main/AZUS-MN.sh">AZUS-MN.sh</a> script that is your MainNode.

# Guide of use AZUS MN for MainNode:

##### For Ubuntu 18.04 / 20.04
```
wget -q https://raw.githubusercontent.com/AzusNodes/AZUS-MNScript/main/AZUS-MN.sh
sudo chmod +x AZUS-MN.sh
./AZUS-MN.sh
```


***

# Guide for Install MultiMN:

Install the multimn script 

`curl -sL https://raw.githubusercontent.com/AzusNodes/AZUS-MultiMN/main/multimn_install.sh | sudo -E bash -`

Add the coin profile.
```
wget -q https://raw.githubusercontent.com/AzusNodes/AZUS-MultiMN/main/profiles/azus.mn
multimn profadd azus.mn azus
```
Now the azus profile is saved and the downloaded file can be removed if you want: `rm -rf azus.dmn`

Stop the azus Service:
```
azus-cli stop
systemctl stop azus
```
Now create 3 extra instances with bootstrap (Ex. You want to make 3 Masternode):
```
multimn install azus --bootstrap
multimn install azus --bootstrap
multimn install azus --bootstrap
```
You can check every MN like this:
```
azus-cli-1 getinfo
azus-cli-2 getinfo
azus-cli-3 getinfo
azus-cli-all getinfo
```
There's also a `azus-cli-0`, that is a reference to the 'main node', not a created one with multimn.

Now, if you want to uninstall any instances,then just uninstall it with:

`multimn uninstall azus 2` (Uninstall instance 2)

You can uninstall all of them with:

`multimn uninstall azus all`


You can get priv key of all MN with:

`multimn list azus --privkey`


Note this all priv key and make `masternode.conf` in your Coldwallet where you done MasternodeTx.
so `masternode.conf` look like this:
```
MN0 IP:50322 MN_PrivKey Tx_Hash Output_Index
MN01 IP:50322 MN_PrivKey Tx_Hash Output_Index
MN02 IP:50322 MN_PrivKey Tx_Hash Output_Index
MN03 IP:50322 MN_PrivKey Tx_Hash Output_Index
```

Here IP and port Same for all MN.

MN0 is your main_node MN which you create with <a href="https://github.com/AzusNodes/AZUS-MNScript/blob/main/AZUS-MN.sh">AZUS-MN.sh</a> script.

MN01, MN02, MN03 is your masternode which you create with multimn.


Now StartMasternode from Coldwallet with:
```
startmasternode alias false MN0
startmasternode alias false MN01
startmasternode alias false MN02
startmasternode alias false MN03
```

Now StartMasternode in VPS with Service:

`systemctl start azus` (Start your MN which is create with main_node <a href="https://github.com/AzusNodes/AZUS-MNScript/blob/main/AZUS-MN.sh">AZUS-MN.sh</a> script)

Below 3 MN which is create with `multimn` script.
```
systemctl start   azus-1.service
systemctl start   azus-2.service
systemctl start   azus-3.service
```

That's all now your MN start.
