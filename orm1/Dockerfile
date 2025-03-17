# Step 1: Use the official Python image as a base
FROM python:3.11-slim

# Step 2: Set the working directory inside the container
WORKDIR /app

# Step 3: Install system dependencies (including SSH)
RUN apt-get update && apt-get install -y openssh-server && rm -rf /var/lib/apt/lists/*

# Step 4: Create SSH directory and configure root access
RUN mkdir /var/run/sshd
RUN echo 'root:Docker!2024' | chpasswd
RUN sed -i 's/^#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# Step 5: Copy requirements and install dependencies
COPY ./orm1/requirements.txt /app/requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Step 6: Copy the rest of the backend code into the container
COPY orm1 /app

# Step 7: Expose necessary ports (Django + SSH)
EXPOSE 8000 2222

# Step 8: Run SSH and Django together
CMD service ssh start && gunicorn --bind 0.0.0.0:8000 orm1.wsgi:application
