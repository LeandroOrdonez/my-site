+++
title = "Common procedures and troubleshooting"
date = 2019-11-11T20:29:41+01:00
draft = false
tags = ["troubleshooting", "programming", "yak shaving"]
categories = ["Programming", "Data management", "Research"]
+++

{{< figure src="/images/ideas/yak-shaving.jpg" caption="Photo by [Lieve Ransijn](https://unsplash.com/@lievemax) on [Unsplash](https://unsplash.com/photos/FsJ_vzp_NI4)" >}} 
This is a categorized list of "*curated*" pointers I have found handy in my long coding sessions (a major part of which I still spend [yak shaving](https://www.techopedia.com/definition/15511/yak-shaving) someone else's code).

### Angular related:
* [Reloading current route in Angular 5 / Angular 6 (reload component when clicking browser's back button)](https://medium.com/engineering-on-the-incline/reloading-current-route-on-click-angular-5-1a1bfc740ab2)
* [Angular material datatable example (sortable, selectable and filterable)](https://stackblitz.com/edit/angular-material2-table?file=app%2Fapp.component.ts)
* [Angular material checkbox + forms example](https://stackblitz.com/edit/angular-tyfg2z?file=app%2Fapp.component.ts)
* [How to prevent robots from crawling an Angular application](https://jeffshamley.com/blogs/how-block-robots-crawling-your-angular-application)
* [`ng-number-picker`](https://www.npmjs.com/package/ng-number-picker)

### Data analysis in Python:
* [`Matplotlib`: Save images in high quality (EPS, PDF)](https://stackoverflow.com/questions/16183462/saving-images-in-python-at-a-very-high-quality)
* [`Matplotlib`: Prevent plot labels from getting cut off when saving them](https://stackoverflow.com/questions/21288062/second-y-axis-label-getting-cut-off/21288063)
* [`Matplotlib`: How to put the legend out of the plot](https://stackoverflow.com/a/4701285/2412831)
* [`Matplotlib`: Reverse the order of legend](https://stackoverflow.com/q/34576059/2412831)
* [`Matplotlib`: Read the data and plotting with multiple markers](https://pydatascience.org/2017/12/05/read-the-data-and-plotting-with-multiple-markers/)
* [`Matplotlib`: Using matplotlib in jupyter notebooks — comparing methods and some tips (`%matplotlib <>`)](https://medium.com/@1522933668924/using-matplotlib-in-jupyter-notebooks-comparing-methods-and-some-tips-python-c38e85b40ba1)
* [`python re`: Non-capturing groups](https://stackoverflow.com/questions/18425386/re-findall-not-returning-full-match)
* [`pip 10 and apt`: How to avoid “Cannot uninstall X” errors for distutils packages
](https://stackoverflow.com/a/50396798/2412831)
* [`scipy & scikit-learn`: How to calculate Silhouette Score of the scipy's fcluster using scikit-learn silhouette score?](https://stackoverflow.com/a/28187426/2412831)
* [`pandas`: How to read a large csv file in chunks](https://stackoverflow.com/a/29334672/2412831)
* [`pandas`: Parallel operations over a pandas DataFrame](https://www.kaggle.com/gvyshnya/parallel-operations-over-a-pandas-df)
* [`pandas`: Random selection per group](https://stackoverflow.com/a/22477520/2412831)
* [`folium`: Map Tiles](https://deparkes.co.uk/2016/06/10/folium-map-tiles/)
* [`folium`: Gallery of examples](https://nbviewer.jupyter.org/github/python-visualization/folium/tree/master/examples/)
* [`folium`: Marker cluster](https://nbviewer.jupyter.org/github/python-visualization/folium/blob/master/examples/MarkerCluster.ipynb)
* [`GeoPandas`: Label Polygons (see second answer)](https://stackoverflow.com/q/38899190/2412831)
* [`GeoPandas`: An Approach for Checking Overlaps and Gaps in Polygons using Geopandas](https://medium.com/@achm.firmansyah/an-approach-for-checking-overlaps-and-gaps-in-polygons-using-geopandas-ebd6606e7f70)
* [`GeoPandas`: R-tree Spatial Indexing with Python (bounding box matches vs exact polygon matches)](https://geoffboeing.com/2016/10/r-tree-spatial-index-python/)
* [`GeoPandas`: Nearest Neighbour Analysis (Nearest polygon to point)](https://automating-gis-processes.github.io/2017/lessons/L3/nearest-neighbour.html)
* [`ipyleaflet`: Get coordinates out of map drawings](https://github.com/jupyter-widgets/ipyleaflet/issues/290)
* [`Jupyter` How to check the source code of a module](https://stackoverflow.com/a/40941511/2412831)
* [`Geoalchemy2`: query all users within X meteres](https://stackoverflow.com/q/20803878/2412831)
* [`pandas`: Normalize semi-structured JSON data into a flat table](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.io.json.json_normalize.html)
* [Streaming data from Postgres into Python](https://stackoverflow.com/a/22002048/2412831)
* [Creating a grid based on GeoHashes](https://blog.tafkas.net/2018/09/28/creating-a-grid-based-on-geohashes/)
* [Time series distances: Dynamic Time Warping (DTW) ](https://github.com/wannesm/dtaidistance)
* [Running `Flask` in production with Docker](https://medium.com/@smirnov.am/running-flask-in-production-with-docker-1932c88f14d0)

### Docker & Kubernetes related:
* [How To Build a Node.js Application with Docker](https://www.digitalocean.com/community/tutorials/how-to-build-a-node-js-application-with-docker)
* [Starting a shell in the Docker Alpine container](https://stackoverflow.com/a/35689633/2412831)
* [How To Share Data between Docker Containers](https://www.digitalocean.com/community/tutorials/how-to-share-data-between-docker-containers#step-1-%E2%80%94-creating-an-independent-volume)
* [Docker Compose for Data Science (Jupyter + PostgreSQL)](https://www.andrewmahon.info/blog/docker-compose-data-science/)
* [`kubectl`: Pull docker image from private repository](https://github.com/kubernetes/kubernetes/issues/41536#issuecomment-280354231)
* [Running `PostgreSQL` using Docker Compose (with persistent volume)](https://linuxhint.com/run_postgresql_docker_compose/)
* [Using `docker-compose`, how to execute multiple commands](https://stackoverflow.com/a/30064175/2412831)
* [Automatically build and push Docker images using GitLab CI](https://angristan.xyz/build-push-docker-images-gitlab-ci/)
* [`k8s`: Pull an Image from a Private Registry](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/)
* [`k8s`: Configure persistent volume storage](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/)
* [`K8s`, `juju`: Kubernetes Core bundle](https://jaas.ai/kubernetes-core/bundle/815)
* [`K8S`, `juju`: Restart K8s related services manually (for the juju bundle)](https://github.com/charmed-kubernetes/bundle/issues/357#issuecomment-316542831)

### Git related
* [Remove submodule](https://stackoverflow.com/a/16162000/2412831)

### Hadoop related:
#### Decommisioning Hadoop datanodes:
* [Decommissioning slave nodes - IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/en/SSPT3X_4.1.0/com.ibm.swg.im.infosphere.biginsights.admin.doc/doc/iop_decom_nodes.html)
* [Decommissioning DataNodes Using the Command Line - Cloudera](https://www.cloudera.com/documentation/enterprise/5-9-x/topics/cdh_ig_decommision_datanodes.html)

#### Fix connection issues between the namenode and datanodes:
* [`Connection Refused`](https://wiki.apache.org/hadoop/ConnectionRefused)

### KafKa related:

* [`Kafka Streams`: How to compute an (windowed) average?](https://cwiki.apache.org/confluence/display/KAFKA/Kafka+Stream+Usage+Patterns)
* [`Kafka Streams`: Write a Kafka Streams Application](https://kafka.apache.org/23/documentation/streams/tutorial)
* [`KSQL`: `ksql-python` A python wrapper for the KSQL REST API](https://github.com/bryanyang0528/ksql-python)

### LaTeX related:
* [Large braces for specifying values of variables by condition](https://tex.stackexchange.com/a/9068)

### PostgreSQL related:
* [`CREATE STATISTICS`: The Postgres 10 feature you didn't know about](https://www.citusdata.com/blog/2018/03/06/postgres-planner-and-its-usage-of-statistics/)
* [PostgreSQL `Explain` Visualizer](http://tatiyants.com/pev/)
* [The Internals of PostgreSQL: Ch. 3 Query Processing (See subsection 3.2.2.2 on `run cost` and `selectivity`)](http://www.interdb.jp/pg/pgsql03.html)
* [Using `date_trunc` to group by hour with a timestamp field?](https://stackoverflow.com/a/42118080/2412831)
* [Insert trigger to Update another table using PostgreSQL](https://stackoverflow.com/questions/12343984/insert-trigger-to-update-another-table-using-postgresql)

### Spark related:
* [On why large executor memory does not imply better performance](https://community.hortonworks.com/questions/144181/num-executors-and-executor-memory-in-spark.html)
* [On the `spark.sql.autoBroadcastJoinThreshold` setting - SparkSQL](https://community.hortonworks.com/questions/144181/num-executors-and-executor-memory-in-spark.html)
* [Shuffle Hash and Sort Merge Joins in Apache Spark](https://sujithjay.com/spark-sql/2018/06/28/Shuffle-Hash-and-Sort-Merge-Joins-in-Apache-Spark/)
* [Broadcast Hash Joins in Apache Spark](https://sujithjay.com/spark-sql/2018/02/17/Broadcast-Hash-Joins-in-Apache-Spark/)
* [Understanding Apache Spark on YARN](https://sujithjay.com/2018/07/24/Understanding-Apache-Spark-on-YARN/)
* [Pyspark: Split multiple array columns into rows (`explode` method)](https://stackoverflow.com/a/41027619/2412831)
* [Convert comma separated string to array in pyspark dataframe](https://stackoverflow.com/a/38189294/2412831)

### Ubuntu related:
* [How To Add Swap Space on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-18-04)
* [Disable automount](https://help.ubuntu.com/community/Mount/USB)
