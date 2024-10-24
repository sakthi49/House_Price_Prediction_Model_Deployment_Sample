# Create Python environment
conda create -n house python=3.11 -y
# Activate the respective environment
conda activate house

# Download the required packages by downloading the below command
pip install -r requirements.txt

# Run the Script to train the model
python model_training.py


You should be able to find the .pkl file (linear_regression_model.pkl) in the model/ directory.

Use FastAPI to build an API to serve model predictions and containerize it using Docker.

# Building the Docker Image
Build the Docker image by running the following docker build command:

docker buildx build -t house-price-prediction-api .

In this command:
. represents the current directory as the build context, which should contain your Dockerfile.
If your Dockerfile is in a different directory, replace . with the path to that directory.

Few things you can check if it doesn't work as expected:

1. Make sure the container was built successfully: Before running, ensure the image exists by listing your Docker images:

docker images

2. Check if port 80 is exposed in the Dockerfile: Ensure your Dockerfile includes a line like:
EXPOSE 80

If your application listens on a different port internally, adjust the run command to map that port instead of 80:80.

3. Check if the container is running: After running the command, verify that the container started successfully:
docker ps

4. Check logs for issues: If the container stops or does not behave as expected, inspect the logs to debug:
docker logs <container_id>

Tagging and Pushing the Image to Docker Hub
1. First, login to Docker Hub:
docker login
2. Tag the Docker image:
docker tag house-price-prediction-api your_username/house-price-prediction-api:v1
3. Push the image to Docker Hub:
docker push your_username/house-price-prediction-api:v1

# Other developers can now pull and run the image like so:

$ docker pull your_username/house-price-prediction-api:v1
$ docker run -d -p 80:80 your_username/house-price-prediction-api:v1