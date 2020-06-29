This article will help you to run elasticsearch on raspberry pi device
Raspberry pi: The Raspberry Pi is a low cost ,credit-card sized computer that plugs into a computer monitor or TV, and uses a standard keyboard and mouse. It is a capable little device that enables people of all ages to explore computing, and to learn how to program in languages like Scratch and Python. It’s capable of doing everything you’d expect a desktop computer to do, from browsing the internet and playing high-definition video, to making spreadsheets, word-processing, and playing games.
Elasticsearch: The open source, distributed, RESTful, JSON-based search engine. Easy to use, scalable and flexible, it earned hyper-popularity among users and a company formed around it, you know, for search.
 we start by ensuring java is install.
First check java install and version on raspberry pi 
java --version 
 
If java is install on your system its good if not check the bellow step to install
ensure all our packages are up to date:
sudo apt-get update
This will update all the packages on your system, ensuring that you have what you need. Once that is in place, it will be necessary to install Java as the runtime environment is necessary. To do this, run:
 sudo apt-get install default-jre
Checkout the path of java where it installed
which java
 

Now once its confirmed that java is properly installed and working lets start elasticsearch download and installation
Click on link to download elasticsearch https://www.elastic.co/downloads/elasticsearch-no-jdk and then download linux installation file. 
 
Once its download extract the file 
 

Now go to the bin folder in elasticsearch and let’s try to execute elasticsearch it will give following error because we are using no jdk bundle so we need to provide java home location to it.  

 

So we will  create symlink for java 
Symbolic links: symbolic path indicating the abstract location of another file.
Look the content in the elasticsearch folder
ls -ltrh
 
Now make jdk directory in the elasticsearch folder 
mkdir jdk
 
Soft links(symlink) are created with the ln command 
ln –s /usr/bin/ /home/pi/Downloads/elaticsearch/jdk/
ln –s originalLocation syslinkLocation 
 

Go to jdk directory and fire ls -ltrh cmd you could see the bin folder showing link to the bin directory  
 

Now java is set for elasticsearch execution but before that check you have allocated proper ram to elasticsearch.for that you need to go to config folder and check in   jvm.options file .if its not allocated properly elastic will not run so make sure you edit the default config as per your needs.
Defaluts memory allocated to the elasticsearch in jvm.options file
 
So I edited  as per ram available on my device  

There is also one more thing that x-pack machine learing is not supported in linux-arm so you need to disable that in elasticsearch.yml file  
So in the elasticsearch.yml file which is in the config directory paste the following line at the end of file
xpack.ml.enabled:false
 
So now your all set to go.go to bin directory in elaticsearch and fire following command
./elasticsreach
In middle you find this line node started and initialized so it stared properly 
 
Check if it’s started properly fire the flowing cmd 
curl http://127.0.0.1:9200
 
If you find any difficult please be free to share your errors and comments to Instagram rushab_ambre

