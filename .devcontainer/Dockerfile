FROM ubuntu:24.04
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get upgrade && apt-get install -y \
    python3-pip curl unzip graphviz git
RUN pip install --upgrade pip
WORKDIR /app
COPY requirements.txt .
# Swap tensorflow for the Metal-accelerated Mac build
RUN pip install tensorflow-macos tensorflow-metal
RUN pip install -r requirements.txt
ENV PYTHONPATH="/app"