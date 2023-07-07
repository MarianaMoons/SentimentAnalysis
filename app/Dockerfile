# Use the official Miniconda base image
FROM continuumio/miniconda3

# Set the working directory
WORKDIR /app

# Copy the code files into the container
COPY environment.yml /app/environment.yml

# Install system dependencies
RUN apt-get update && apt-get install -y curl gnupg

# Install Bazel
RUN curl https://bazel.build/bazel-release.pub.gpg | apt-key add -
RUN echo "deb [arch=amd64] https://storage.googleapis.com/bazel-apt stable jdk1.8" | tee /etc/apt/sources.list.d/bazel.list
RUN apt-get update && apt-get install -y bazel=5.4.0

# Create a Conda environment and activate it
RUN conda env create -f environment.yml
RUN echo "source activate myenv" > ~/.bashrc
ENV PATH /opt/conda/envs/myenv/bin:$PATH

# Set environment variables
ENV PYTHONPATH=/app/models/research/seq_flow_lite:$PYTHONPATH

# Build the SeqFlow Lite library
RUN git clone https://www.github.com/tensorflow/models /app/models
RUN cd /app/models/research/seq_flow_lite/demo/colab && ./setup_workspace.sh
RUN pip install /app/models/research/seq_flow_lite
RUN rm -rf /app/models/research/seq_flow_lite/tf_ops
RUN rm -rf /app/models/research/seq_flow_lite/tflite_ops




