# Continuous Integration and Deployment with AWS Elastic Beanstalk and Travis CI

## Project FLOW

### **DEV**

1. Create/change features
2. Make changes on non-master branch

> Push to Github, create PR to merge with master

### **TEST**

1. Code pushed to Travis CI
2. Test run

> Merge PR with master

### **PROD**

1. Code pushed to Travis CI
2. Tests run
3. Deploy to AWS Elastic Beanstalk

---

# Development Environment

## Dockerfile.dev

1. Get the image needed
2. Creates a working directory
3. Copies package.json from root dir
4. Runs npm install
5. Copies all files from root dir
6. Runs command 'npm run start'

## Docker-Compose file

1. Builds two 'Services', a web service and a test service
2. The `volumes` param is like a --watch on certain dirs
3. Noice how we give the second service **tests** a new command to run

---

# Production Environment using Nginx

`Note: Nginx is used to handle server requests inside our container`

## Build Phase

1. Uses node:alpine
2. Copy package.json
3. Install dependencies
4. Run 'npm run build'

## Run Phase

1. Uses nginx
2. Exposes a port (default is 80)
3. Copy --from=builder (our named first build) /app/build /usr/share/nginx/html

`All the extra stuff created in the Build Phase that we didn't bring over is gonzo`

---
