### Stage Setup
1. Let’s get started by first cloning the demo code repository, changing the working directory, and checking the demo branch out.
![01](img1.png)

### Step 0: Basic Link Extractor Script
1. Checkout the step0 branch and list files in it.
![02](img2.png)
2. The linkextractor.py file is the interesting one here, so let’s look at its contents:
![03](img3.png)
3. However, this seemingly simple script might not be the easiest one to run on a machine that does not meet its requirements. The README.md file suggests how to run it, so let’s give it a try:
![04](img4.png)
4. When we tried to execute it as a script, we got the Permission denied error. Let’s check the current permissions on this file:
![05](img5.png)
5. We can either change it by running chmod a+x linkextractor.py or run it as a Python program instead of a self-executing script as illustrated below:
![06](img6.png)

### Step 1: Containerized Link Extractor Script
1. Checkout the step1 branch and list files in it.
![07](img7.png)
2. We have added one new file (i.e., Dockerfile) in this step. Let’s look into its contents:
![08](img8.png)
3. So far, we have just described how we want our Docker image to be like, but didn’t really build one. So let’s do just that:
![09](img9.png)
4. We have created a Docker image named linkextractor:step1 based on the Dockerfile illustrated above. If the build was successful, we should be able to see it in the list of image:
![10](img10.png)
5. Now, let’s run a one-off container with this image and extract links from some live web pages:
![11](img11.png)
6. Let’s try it on a web page with more links in it:
![12](img12.png)

### Step 2: Link Extractor Module with Full URI and Anchor Text
1. Checkout the step2 branch and list files in it.
![13](img13.png)
2. Let’s have a look at the updated script:
![14](img14.png)
3. Now, let’s build a new image and see these changes in effect:
![15](img15.png)
4. We have used a new tag linkextractor:step2 for this image so that we don’t overwrite the image from the step1 to illustrate that they can co-exist and containers can be run using either of these images.
![16](img16.png)
5. Running a one-off container using the linkextractor:step2 image should now yield an improved output:
![17](img17.png)
6. Running a container using the previous image linkextractor:step1 should still result in the old output:
![18](img18.png)

### Step 3: Link Extractor API Service
1. Checkout the step3 branch and list files in it.
![19](img19.png)
2. Let’s first look at the Dockerfile for changes:
![20](img20.png)
3. The linkextractor.py module remains unchanged in this step, so let’s look into the newly added main.py file:
![21](img21.png)
4. It’s time to build a new image with these changes in place:
![22](img22.png)
5. We are also assigning a name (--name=linkextractor) to the container to make it easier to see logs and kill or remove the container.
![23](img23.png)
6. If things go well, we should be able to see the container being listed in Up condition:
![24](img24.png)
7. We can now make an HTTP request in the form /api/<url> to talk to this server and fetch the response containing extracted links:
![25](img25.png)
8. Since the container is running in detached mode, so we can’t see what’s happening inside, but we can see logs using the name linkextractor we assigned to our container:
![26](img26.png)
9. We can see the messages logged when the server came up, and an entry of the request log when we ran the curl command. Now we can kill and remove this container:
![27](img27.png)

### Step 4: Link Extractor API and Web Front End Services
1. Checkout the step4 branch and list files in it.
![28](step4-checkout.png)
2. So let’s look at the docker-compose.yml file we have:
![29](step4-composeyml.png)
3. Now, let’s have a look at the user-facing www/index.php file:
![30](step4-cat_index.png)
4.Let’s bring these services up in detached mode using docker-compose utility:
![31](step4-compose-build.png)
5. We should now be able to talk to the API service as before:
![32](step4-curl-link.png)
6. Before we move on to the next step we need to shut these services down, but Docker Compose can help us take care of it very easily:
![33](step4-docker-down.png)

### Step 5: Redis Service for Caching
1. Checkout the step5 branch and list files in it.
![34](step5-checkout.png)
2. Let’s first inspect the newly added Dockerfile under the ./www folder:
![35](step5-cat-dockerfle.png)
3. Next, we will look at the API server’s api/main.py file where we are utilizing the Redis cache:
![36](step5-cat-mainpy.png)
4. Now, let’s look into the updated docker-compose.yml file:
![37](step5-cat-composeyml.png)
5. Let’s boot these services up:
![38](step5-compose-up.png)
6.  we can use docker-compose exec followed by the redis service name and the Redis CLI’s monitor command:
![39](step5-docker-exec-redis.png)
7. Now, shut these services down and get ready for the next step:
![40](step5-compose-down.png)

### Step 6: Swap Python API Service with Ruby
1. Checkout the step6 branch and list files in it.
![41](step6-checkout.png)
2. With these in place, let’s boot our service stack:
![42](step6-compose-up.png)
3. We should now be able to access the API (using the updated port number):
![43](step6-curl-link.png)
4. We can use the tail command with the -f or --follow option to follow the log output live.
![44](step6-cat-log.png)
5. Since we have persisted logs, they should still be available after the services are gone:
![45](step6-linkextractor.png)
