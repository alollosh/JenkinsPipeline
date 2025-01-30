# Use a Python base image
FROM python:3.9-slim

# Set the working directory
WORKDIR /app

# Copy the current directory contents into the container
COPY . /app

# Install dependencies
RUN pip install Flask

# Expose the port
EXPOSE 5000

# Run the application
CMD ["python", "webapp.py"]
