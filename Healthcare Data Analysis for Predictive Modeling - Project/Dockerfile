# Use the official Apache Spark image as the base image
FROM bitnami/spark:latest

# Install necessary packages for Jupyter
USER root
RUN apt-get update && \
    apt-get install -y python3-pip && \
    pip3 install --no-cache-dir jupyter py4j numpy boto3 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*



# Set the environment variables for Jupyter Notebook
ENV JUPYTER_PORT=8888

# Expose the Jupyter port
EXPOSE ${JUPYTER_PORT}

# Copy the Jupyter Notebook into the image
COPY process_data.ipynb /home/jovyan/process_data.ipynb


# Set the working directory
WORKDIR /home/jovyan


# Start the Jupyter Notebook and Spark
CMD ["sh", "-c", "jupyter notebook --ip=0.0.0.0 --port=${JUPYTER_PORT} --no-browser --allow-root --NotebookApp.token='' --NotebookApp.password='' & /opt/bitnami/spark/bin/spark-class org.apache.spark.deploy.master.Master"]
