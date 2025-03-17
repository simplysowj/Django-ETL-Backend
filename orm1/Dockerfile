# Step 1: Use the official Python image as a base
FROM python:3.11-slim

# Step 2: Set the working directory inside the container
WORKDIR /app

# Step 3: Copy the requirements file into the container
COPY backend/apiview/orm1/requirements.txt /app/requirements.txt


Copy
# Copy the requirements file
COPY ./orm1/requirements.txt /app/requirements.txt

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application code
COPY ./orm1 /app

# Step 6: Expose port 8000 for the Django app
EXPOSE 8000

# Step 7: Set environment variables for Python
ENV PYTHONUNBUFFERED=1

# Step 8: Run Django migrations and start the app
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "orm1.wsgi:application"]
