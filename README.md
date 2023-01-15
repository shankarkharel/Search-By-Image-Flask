# Simple Image Search Engine


## [Demo](http://www.simple-image-search.xyz/)
![](http://yusukematsui.me/project/sis/img/screencapture2.jpg)

## Workflow
![](http://yusukematsui.me/project/sis/img/overview.png)


## Overview
- Simple image-based image search engine using Keras + Flask. You can launch the search engine just by running two python scripts.
- `offline.py`: This script extracts a deep-feature from each database image. Each feature is a 4096D fc6 activation from a VGG16 model with ImageNet pre-trained weights.
- `server.py`: This script runs a web-server. You can send your query image to the server via a Flask web-interface. The server finds similar images to the query by a simple linear scan.
- GPUs are not required.
- Tested on Mac Os(M1)

## Links
- [Demo](http://www.simple-image-search.xyz/)

## Usage
```bas
git clone https://github.com/matsui528/sis.git
cd sis
pip install -r requirements.txt

# Put your image files (*.jpg) on static/img

# Then fc6 features are extracted and saved on static/feature
# Note that it takes time for the first time because Keras downloads the VGG weights.
python offline.py

# Now you can do the search via localhost:5000
python app.py
```

## Advanced: Launch on AWS EC2
- You can easily launch the search engine server on AWS EC2. Please first open the port 5000 and launch an EC2 instance. Note that you need to create a security group such that the port 5000 is opened.
- A middle-level CPU instance is sufficient, e.g., m5.large.
- After you log-in to the instance by ssh, please setup the python environment (e.g., by [anaconda](https://docs.anaconda.com/anaconda/install/linux/)).
- Run `offline.py` and `server.py`.
- After you run `python server.py`, you can access the server from your browser via something like `http://ec2-XX-XX-XXX-XXX.us-west-2.compute.amazonaws.com:5000`
- (Advanced) If you'd like to deploy the system in a secure way, please consider running the search engine with the usual web server, e.g., uWSGI + nginx.


## Citation

    @misc{sis,
	    author = {Shankar Kharel},
	    title = {Simple Image Search Engine},
    }


## Waleeds project

Auto reloading python Flask app upon code changes:
Type this in the terminal  FLASK_APP=app.py FLASK_ENV=development flask run

[Stackoverflow](https://stackoverflow.com/questions/16344756/auto-reloading-python-flask-app-upon-code-changes)
