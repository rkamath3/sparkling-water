FROM harbor.h2o.ai/opsh2oai/h2o-3-hadoop-hdp-2.2:47

ENV LANG 'C.UTF-8'
RUN locale

RUN rm -rf /etc/hadoop/conf/yarn-site.xml
COPY conf/yarn-site.xml /etc/hadoop/conf/yarn-site.xml

RUN \
    rm /etc/startup/50_hive_start && \
    rm /etc/startup/70_start_slapd

RUN \
    apt-get update && apt-get install apt-transport-https && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9 && \
    add-apt-repository 'deb [arch=amd64,i386] https://cran.rstudio.com/bin/linux/ubuntu xenial/'


RUN apt-get update && apt-get install -y git npm curl zip s3cmd r-base r-base-dev libxml2-dev libssl-dev libcurl4-openssl-dev

RUN \
    curl -sL https://deb.nodesource.com/setup_11.x | sudo -E bash - && \
    sudo apt-get install -y nodejs

RUN \
    R -e 'install.packages("xml2", repos = "http://cran.us.r-project.org")' && \
    R -e 'install.packages("openssl", repos = "http://cran.us.r-project.org")' && \
    R -e 'install.packages("httr", repos = "http://cran.us.r-project.org")' && \
    R -e 'install.packages("bitops", repos = "http://cran.us.r-project.org")' && \
    R -e 'install.packages("RCurl", repos = "http://cran.us.r-project.org")' && \
    R -e 'install.packages("jsonlite", repos = "http://cran.us.r-project.org")' && \
    R -e 'install.packages("testthat", repos = "http://cran.us.r-project.org")' && \
    R -e 'install.packages("dplyr", repos = "http://cran.us.r-project.org")' && \
    R -e 'install.packages("devtools", repos = "http://cran.us.r-project.org")' && \
    R -e 'install.packages("usethis", repos = "http://cran.us.r-project.org")' && \
    R -e 'install.packages("sparklyr", repos = "http://cran.us.r-project.org")'

###
###  Prepare Spark
###

RUN cd /home/jenkins && \
    wget http://mirrors.ocf.berkeley.edu/apache/spark/spark-2.4.0/spark-2.4.0-bin-hadoop2.7.tgz  && \
    mkdir -p spark-2.4.0-bin-hadoop2.7 &&  \
    tar zxvf spark-2.4.0-bin-hadoop2.7.tgz -C spark-2.4.0-bin-hadoop2.7 --strip-components 1 && \
    rm -rf spark-2.4.0-bin-hadoop2.7.tgz

RUN cd /home/jenkins && \
    wget http://mirrors.ocf.berkeley.edu/apache/spark/spark-2.3.2/spark-2.3.2-bin-hadoop2.7.tgz  && \
    mkdir -p spark-2.3.2-bin-hadoop2.7 &&  \
    tar zxvf spark-2.3.2-bin-hadoop2.7.tgz -C spark-2.3.2-bin-hadoop2.7 --strip-components 1 && \
    rm -rf spark-2.3.2-bin-hadoop2.7.tgz

RUN cd /home/jenkins && \
    wget http://archive.apache.org/dist/spark/spark-2.3.1/spark-2.3.1-bin-hadoop2.7.tgz  && \
    mkdir -p spark-2.3.1-bin-hadoop2.7 &&  \
    tar zxvf spark-2.3.1-bin-hadoop2.7.tgz -C spark-2.3.1-bin-hadoop2.7 --strip-components 1 && \
    rm -rf spark-2.3.1-bin-hadoop2.7.tgz

RUN cd /home/jenkins && \
    wget http://archive.apache.org/dist/spark/spark-2.3.0/spark-2.3.0-bin-hadoop2.7.tgz  && \
    mkdir -p spark-2.3.0-bin-hadoop2.7 &&  \
    tar zxvf spark-2.3.0-bin-hadoop2.7.tgz -C spark-2.3.0-bin-hadoop2.7 --strip-components 1 && \
    rm -rf spark-2.3.0-bin-hadoop2.7.tgz

RUN cd /home/jenkins && \
    wget http://mirrors.ocf.berkeley.edu/apache/spark/spark-2.2.2/spark-2.2.2-bin-hadoop2.7.tgz  && \
    mkdir -p spark-2.2.2-bin-hadoop2.7 &&  \
    tar zxvf spark-2.2.2-bin-hadoop2.7.tgz -C spark-2.2.2-bin-hadoop2.7 --strip-components 1 && \
    rm -rf spark-2.2.2-bin-hadoop2.7.tgz

RUN cd /home/jenkins && \
    wget http://archive.apache.org/dist/spark/spark-2.2.1/spark-2.2.1-bin-hadoop2.7.tgz  && \
    mkdir -p spark-2.2.1-bin-hadoop2.7 &&  \
    tar zxvf spark-2.2.1-bin-hadoop2.7.tgz -C spark-2.2.1-bin-hadoop2.7 --strip-components 1 && \
    rm -rf spark-2.2.1-bin-hadoop2.7.tgz

RUN cd /home/jenkins && \
    wget http://archive.apache.org/dist/spark/spark-2.2.0/spark-2.2.0-bin-hadoop2.7.tgz  && \
    mkdir -p spark-2.2.0-bin-hadoop2.7 &&  \
    tar zxvf spark-2.2.0-bin-hadoop2.7.tgz -C spark-2.2.0-bin-hadoop2.7 --strip-components 1 && \
    rm -rf spark-2.2.0-bin-hadoop2.7.tgz

RUN cd /home/jenkins && \
    wget http://mirrors.ocf.berkeley.edu/apache/spark/spark-2.1.3/spark-2.1.3-bin-hadoop2.7.tgz  && \
    mkdir -p spark-2.1.3-bin-hadoop2.7 &&  \
    tar zxvf spark-2.1.3-bin-hadoop2.7.tgz -C spark-2.1.3-bin-hadoop2.7 --strip-components 1 && \
    rm -rf spark-2.1.3-bin-hadoop2.7.tgz

RUN cd /home/jenkins && \
    wget http://archive.apache.org/dist/spark/spark-2.1.2/spark-2.1.2-bin-hadoop2.7.tgz  && \
    mkdir -p spark-2.1.2-bin-hadoop2.7 &&  \
    tar zxvf spark-2.1.2-bin-hadoop2.7.tgz -C spark-2.1.2-bin-hadoop2.7 --strip-components 1 && \
    rm -rf spark-2.1.2-bin-hadoop2.7.tgz

RUN cd /home/jenkins && \
    wget http://archive.apache.org/dist/spark/spark-2.1.1/spark-2.1.1-bin-hadoop2.7.tgz  && \
    mkdir -p spark-2.1.1-bin-hadoop2.7 &&  \
    tar zxvf spark-2.1.1-bin-hadoop2.7.tgz -C spark-2.1.1-bin-hadoop2.7 --strip-components 1 && \
    rm -rf spark-2.1.1-bin-hadoop2.7.tgz

RUN cd /home/jenkins && \
    wget http://archive.apache.org/dist/spark/spark-2.1.0/spark-2.1.0-bin-hadoop2.7.tgz  && \
    mkdir -p spark-2.1.0-bin-hadoop2.7 &&  \
    tar zxvf spark-2.1.0-bin-hadoop2.7.tgz -C spark-2.1.0-bin-hadoop2.7 --strip-components 1 && \
    rm -rf spark-2.1.0-bin-hadoop2.7.tgz

ENV SPARK_HOME_2_4_0 /home/jenkins/spark-2.4.0-bin-hadoop2.7
ENV SPARK_HOME_2_3_2 /home/jenkins/spark-2.3.2-bin-hadoop2.7
ENV SPARK_HOME_2_3_1 /home/jenkins/spark-2.3.1-bin-hadoop2.7
ENV SPARK_HOME_2_3_0 /home/jenkins/spark-2.3.0-bin-hadoop2.7
ENV SPARK_HOME_2_2_2 /home/jenkins/spark-2.2.2-bin-hadoop2.7
ENV SPARK_HOME_2_2_1 /home/jenkins/spark-2.2.1-bin-hadoop2.7
ENV SPARK_HOME_2_2_0 /home/jenkins/spark-2.2.0-bin-hadoop2.7
ENV SPARK_HOME_2_1_3 /home/jenkins/spark-2.1.3-bin-hadoop2.7
ENV SPARK_HOME_2_1_2 /home/jenkins/spark-2.1.2-bin-hadoop2.7
ENV SPARK_HOME_2_1_1 /home/jenkins/spark-2.1.1-bin-hadoop2.7
ENV SPARK_HOME_2_1_0 /home/jenkins/spark-2.1.0-bin-hadoop2.7

USER jenkins

###
### Warm up Gradle caches for Sparkling Water
###
RUN cd /home/jenkins && \
    git clone https://github.com/h2oai/sparkling-water.git && \
    cd sparkling-water && \
    ./gradlew build testClasses resolveTestRuntimeDependencies -PtestMojoPipeline=true -x check -x :sparkling-water-r:build -x :sparkling-water-py:build && \
    cd ..

USER root

### Remove Sparkling Water
RUN cd /home/jenkins && rm -rf sparkling-water

# Change permissions so we can install R packages
RUN chmod 777 /usr/local/lib/R/site-library

USER jenkins

ENV USER jenkins

# Install Conda as we need to publish Sparkling Water as conda package
RUN cd /home/jenkins && \
    wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /home/jenkins/miniconda.sh && \
    bash /home/jenkins/miniconda.sh -b -p /home/jenkins/miniconda && \
    rm /home/jenkins/miniconda.sh

ENV PATH "/home/jenkins/miniconda/bin:${PATH}"

RUN \
    conda install anaconda anaconda-client conda-build -y && \
    conda update conda -y && \
    conda update anaconda anaconda-client conda-build -y


