# Recommender System  
## Clarify/Design Requirements (memory, speed)
* Drop movies or users with low interactions, -> what to do with new users/movies?
* size of user-item matrx, time and space requirement for matrix factorization/KNN 
## Select EC2 Instance Type
* Based on memory requirements and compute requirements, select EC2 instance
* Currently using r5n.8xlarge for the 200 GB RAM
## Setup EC2 Instance to run Jupyter Server 
### Setup EC2
![Security Groups for EC2](https://dataschool.com/assets/images/data-modeling-101/jupyter_article/securityGroups.png)

### Install Anaconda on EC2 

```
$ wget https://repo.anaconda.com/archive/Anaconda3-2019.03-Linux-x86_64.sh
$ bash Anaconda3-2019.03-Linux-x86_64.sh
$ echo "export PATH=/home/ec2-user/anaconda3/bin:$PATH" >> ~/.bashrc
$ source .bashrc
```

### Setup Jupter Notebook Server on EC2
```
$ jupyter notebook --generate-config
$ ipython
```
Generate Sha1 code from password for Jupyter Server log-in
```
>>> from IPython.lib import passwd
>>> passwd()
```
** follow prompts and save output - 'sha1:HASH-COMES-FROM-HERE'

```
cd .jupyter
vim jupyter_notebook_config.py
```
Paste the following code to configure the Jupyter Server
```
conf = get_config()
conf.NotebookApp.ip = '0.0.0.0'
conf.NotebookApp.password = u'sha1:HASH-GOES-HERE'
conf.NotebookApp.open_browser = False
conf.NotebookApp.port = 8888
```
Set configuration to auto-run on server start-up..
```
  $ mkdir MyNotebooks
  $ echo "conda init" >> ~/.bashrc
  $ echo "jupyter notebook" >> ~/.bashrc
  $ source .bashrc
```
### Connect Remotely to Notebook 
* fill-in URL to: http://<your AWS public dns>:8888/ 
* (ex. http://ec2-18-222-233-183.us-east-2.compute.amazonaws.com:8888/)
    
### Credit to:
* https://dataschool.com/data-modeling-101/running-jupyter-notebook-on-an-ec2-server/
* https://jupyter-notebook.readthedocs.io/en/stable/public_server.html
