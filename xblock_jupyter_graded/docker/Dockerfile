FROM python:3.8  
ARG PACKAGES

# Install OpenJDK-11
RUN apt-get update && \
    apt-get install -y openjdk-11-jdk && \
    apt-get install -y ant && \
    apt-get clean;

# Fix certificate issues
RUN apt-get update && \
    apt-get install ca-certificates-java && \
    apt-get clean && \
    update-ca-certificates -f;

# Setup JAVA_HOME -- useful for docker commandline
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk-amd64/
RUN export JAVA_HOME
RUN pip install --upgrade pip && pip install nbgrader==0.6.2
RUN pip install --upgrade nbconvert==5.6.1
RUN pip install --upgrade kotlin-jupyter-kernel>=0.9.1.51
RUN pip install jinja2==2.10.3 --force-reinstall
RUN pip install tornado==6.0.4 --force-reinstall
RUN pip install jupyter-client==6.1.12 --force-reinstall
RUN python3 -m venv /home/temp_env
RUN mkdir -p /home/nbgrader/course/source/ps1 && \
    mkdir -p /etc/jupyter
COPY container.py run_grader.py autograded_checkers.py exceptions.py /home/jupyter/
COPY clearsolutions.py /usr/local/lib/python3.8/site-packages/nbgrader/preprocessors/
