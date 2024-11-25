FROM registry.access.redhat.com/ubi9/python-39:1-117.1684741281

# By default, listen on port 8081
EXPOSE 3000/tcp
ENV DAGSTER_HOME=/app/data

# Mettre à jour pip
RUN pip install --upgrade pip

# Set the working directory in the container
WORKDIR /app

# Copy the content of the local src directory to the working directory
COPY . .

# Install any dependencies
RUN \
  if [ -f requirements.txt ]; \
    then pip install -r requirements.txt; \
  elif [ `ls -1q *.txt | wc -l` == 1 ]; \
    then pip install -r *.txt; \
  fi

USER root
RUN chmod ug+rw -R /app


# Specify the command to run on container start
CMD ["dagster", "dev", "-h", "0.0.0.0", "-p", "3000"]