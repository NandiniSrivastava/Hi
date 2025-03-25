# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Install build dependencies
RUN apt-get update && apt-get install -y \
    gcc \
    build-essential \
    cmake \
    && rm -rf /var/lib/apt/lists/*

# Set the working directory in the container
WORKDIR /app

# Ensure the projects directory exists
RUN mkdir -p /projects

# Copy only requirements.txt first (Better Caching)
COPY requirements.txt /app/

# Upgrade pip and install dependencies
RUN pip install --upgrade pip  
RUN pip install --no-cache-dir -r requirements.txt

# Copy the projects directory
COPY projects /projects

# Copy the rest of the application files
COPY . /app

# Set an environment variable for the projects directory
ENV PROJECTS_DIR=/projects

# Expose the correct port (Streamlit runs on 8501)
EXPOSE 8501

# Run the Streamlit app when the container launches
CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.enableCORS=false", "--server.enableXsrfProtection=false"]
