# Running-TXpipe

git clone --recurse-submodules https://github.com/LSSTDESC/TXPipe

and then install dependencies for it with conda like this on a laptop/desktop (M1 macs are not yet supported, sorry!):

cd TXPipe
./bin/install.sh
You can now set up your environment using:

source ./conda/bin/activate
which you should run each time you start a new terminal, from the TXPipe directory.

Running
Download some test data:

curl -O https://portal.nersc.gov/cfs/lsst/txpipe/data/example.tar.gz
tar -zxvf example.tar.gz

#Now you have to install the depedances; 

pip install ceci  <br /> 
pip install parallel_statistics <br /> 
pip install tables_io<br /> 
pip install qp<br /> 
pip install Qpy<br /> 
 python setup.py egg_info <br /> 
 
 
 pip install threadpoolctl ceci sacc parallel_statistics git+git://github.com/LSSTDESC/gcr-catalogs#egg=GCRCatalogs  git+git://github.com/LSSTDESC/qp git+git://github.com/LSSTDESC/desc_bpz healsparse flexcode  xgboost==1.1.1  git+https://github.com/dask/dask-mpi  git+https://github.com/LSSTDESC/firecrown@v0.4 git+git://github.com/LSSTDESC/desc_bpz git+git://github.com/LSSTDESC/qp 
 
 OR 
  pip install threadpoolctl ceci sacc parallel_statistics git+git://github.com/LSSTDESC/gcr-catalogs#egg=GCRCatalogs  git+git://github.com/LSSTDESC/qp git+git://github.com/LSSTDESC/desc_bpz healsparse flexcode  xgboost==1.1.1  git+git://github.com/dask/dask-mpi  git+git://github.com/LSSTDESC/firecrown@v0.4 git+git://github.com/LSSTDESC/desc_bpz git+git://github.com/LSSTDESC/qp 
 

$pip install delightPZ  #  this one didn't work 


### Make edits to txpipe/blinding.py and adding these lines just before line 70: 

####some kinds of crash like this one can mean that something you have recently printed that is waiting in a buffer to actually appear on the screen doesn't actually make it that far.  This makes sure that anything waiting to be printed gets printed now, before nay crash

import sys
sys.stdout.flush()
sys.stderr.flush()  

####This prints out the data points in the file so we can see if there is anything odd in them
print("**** DATA POINTS ****")
for d in blinded_sack.data:
    print(d)

#### The metadata feels like a place where something might go wrong, because we put lots of different kinds of information in it. So let's print that
print("**** METADATA ****")
for k,v in blinded_sack.metadata.items():
    print(k, v, type(k), type(v))

#### Let's do this again. It can't hurt.
sys.stdout.flush()
sys.stderr.flush()   


Then run a pipeline on that data:

ceci examples/metadetect/pipeline.yml 
