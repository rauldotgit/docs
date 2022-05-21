---
sidebar_position: 2
---

#  How it works: Running A/B test on the server

ABRouter SDKs are working pretty easily. They making the HTTP requests to the ABRouter remote server. You need to send the user identifier and branch uid to run the experiment. The response will contain what branch the user got.

If you don't enable the parallel running for your SDK request will be made synchronously.

Parallel running mode allows you to reduce the time of running the experiment by PHP. 
