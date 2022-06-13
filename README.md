# docker-livy

### Check the article here:  <a href="https://coraspe-ramses.medium.com/building-real-time-interactions-with-apache-spark-through-apache-livy-53169d87d012">Building Real-time communication with Apache Spark through Apache Livy</a>

## Dockerizing and Consuming an Apache Livy environment

<p align="center">
  <img 
    src="https://user-images.githubusercontent.com/8701464/173258291-17f44f56-f206-4da8-a2c7-20b55981191c.png"
  >
</p>

As you can see, In order to reproduce a real example we would need three components:

- Apache Spark Cluster
- Apache Livy Server
- Apache Livy Client

As an additional component I would add docker for a faster implementation, and a PostgreSQL database server to simulate an external data source available for Apache Spark.

## In order to reproduce the experiment we would need to follow the next steps:

- Install Docker Desktop on Windows, it will install Docker Compose as well, Docker Compose will allow you to run multiple container applications.
- Install git-bash for windows, once installed, open git bash and download this repository, this will download the docker-compose.yaml file, and other files needed.

```linux
ramse@DESKTOP-K6K6E5A MINGW64 /c
$ git clone https://github.com/Wittline/docker-livy.git
```

- Once all the files needed were downloaded from the repository, let's run everything. We will use the git bash tool again, go to the folder docker-livy and we will run the Docker Compose command:

```linux
ramse@DESKTOP-K6K6E5A MINGW64 /c
$ cd docker-livy

ramse@DESKTOP-K6K6E5A MINGW64 /c/docker-livy
$ cd code

ramse@DESKTOP-K6K6E5A MINGW64 /c/docker-livy/code
$ cd apps

@DESKTOP-K6K6E5A MINGW64 /c/docker-livy/code/apps
$ docker-compose up -d --build
```

- Wait for a minutes, and when the execution of the last command is finished, use the following command to check the status of all the containers.

```linux
docker ps
```

<p align="center">
  <img 
    src="https://user-images.githubusercontent.com/8701464/173258498-14afc89d-6052-4af1-978b-04be8808a255.png"
  >
</p>

- If everything is up and running then we are going to move forward with other steps to interact with the Apache Livy interface using livyc
- Setiting a local environment with Google Colab
- Go to git-bash and put the next command:

```linux
ramse@DESKTOP-K6K6E5A MINGW64 ~
jupyter notebook --NotebookApp.allow_origin='https://colab.research.google.com' --port=8888 --NotebookApp.port_retries=0
```

- After the execution of the last command, copy the localhost URL, you will need it for colab
- Go to Google Colab
- Create a new Notebook
- Go to -> Connect -> "Connect to local runtime" -> Paste the url copied from the last step and put it in Backend URL -> connect
- Upload the file test-livy.ipynb, and use it into your colab local env:
- Run each cell and see the results on each steps.

Note that among the actions taken in the test-livy.ipynb file, the postgres database is being populated with data using an external .csv file, this in order for apache spark to have data to interact with.

- If you want to monitorize all the session created in Apache Livy Server go to the address: http://localhost:8998/ui

<p align="center">
  <img 
    src="https://user-images.githubusercontent.com/8701464/173258541-1bd310c7-fd9f-4424-a348-d05d17f73f34.png"
  >
</p>


The Python Package <a href="https://github.com/Wittline/livyc">livyc</a> works well to submit pyspark scripts dynamically and asynchronously to the Apache Livy server, this in turn interacts with the Apache Spark Cluster in a transparent way, check this project and remember to check all the files before interacting with the jupyter notebook file.

## Contributing and Feedback
Any ideas or feedback about this repository?. Help me to improve it.

## Authors
- Created by <a href="https://twitter.com/RamsesCoraspe"><strong>Ramses Alexander Coraspe Valdez</strong></a>
- Created on 2022

## License
This project is licensed under the terms of the MIT License.

