# GitHub Actions + Docker: CI Pipeline Demo

This repository shows how to use **GitHub Actions** to build and run a simple Docker container, all **within a CI pipeline**, with **zero cloud dependencies**.

It’s a hands-on demo designed for learners who want to understand:

- How Docker integrates into CI/CD
- How GitHub Actions can build and run containers
- How to automatically test that your container works

---

## What You’ll Learn

By exploring this project, you'll see:

1. How to write a `Dockerfile` for a basic Node.js app  
2. How GitHub Actions builds that image automatically  
3. How it runs the container inside the CI pipeline  
4. How we test the container response with `curl`  

All of this happens **inside GitHub**, without touching AWS, Azure, or any other infrastructure.

---

## What’s Inside?

### The App

Inside this repo, we have a super simple Node.js app (`app.js`) that returns a plain message when you hit it with a browser or curl:

```js
res.end("Hello from Docker in GitHub Actions!");
```

## The Dockerfile

The `Dockerfile` wraps this app into a container image that:

- Uses Node.js 18  
- Installs dependencies  
- Runs the app on port 3000  

---

## The CI Pipeline (GitHub Actions)

When you push code to `main`, the workflow in `.github/workflows/docker-ci.yml` does the following:

### Step-by-Step

**1. Check out the code**  
GitHub pulls down your repo into the runner.

**2. Set up Docker Buildx**  
This allows us to build Docker images reliably in CI.

**3. Build the Docker image**  
It runs `docker build -t demo-app .`

**4. Run the container**  
We start the container in the background on port 3000.

**5. Wait for it to start**  
We give it a few seconds to boot up.

**6. Run a test**  
We use `curl` to make a request to `http://localhost:3000`  
Then we check the response contains the expected message.

**7. Fail if it’s wrong**  
If the message isn’t found, the pipeline fails, just like a real test!

---

## What Success Looks Like

You’ll see something like this in the Actions log:

```
And your workflow will pass
```
---

## What Failure Looks Like

If the app fails or the message changes:
```
Test failed: Unexpected response
Error: Process completed with exit code 1.
```

And the workflow stops there, a clear sign something’s broken.

---

## Why This Matters

In real DevOps pipelines, we want to:

- Know our container builds correctly  
- Confirm it runs without crashing  
- Ensure it returns the right results  

This project simulates that in a **safe, fast, free environment**, and sets you up to scale toward:

- Multi-stage builds  
- Real app tests  
- Publishing to Docker Hub or GitHub Container Registry  
- Deploying to cloud environments like AWS ECS or Azure Container Apps  

---

## Want to Try It?

Fork this repo, make a change (like edit the response message), and push it.

Watch what happens in **Actions**, and see how changing one line can break or pass your pipeline.
