---
title: "Containers"
section: "contribute"
---

# Mattermost Containers

Mattermost uses the [Docker Registry](https://hub.docker.com/u/mattermost) to publish the official images for the Mattermost Server and also for other supporting images that is used for internal/public development and testing

This page will list all the Docker Repositories used by Mattermost and community

- [mattermost/mattermost-enterprise-edition](https://hub.docker.com/r/mattermost/mattermost-enterprise-edition) - **Official Mattermost Server** image for the **Enterprise edition version**. To find the Dockerfile please refer to https://github.com/mattermost/mattermost-server/tree/master/build

- [mattermost/mattermost-team-edition](https://hub.docker.com/r/mattermost/mattermost-team-edition) - **Official Mattermost Server** image for the **Team edition version**. To find the Dockerfile please refer to https://github.com/mattermost/mattermost-server/tree/master/build

- [mattermost/mattermost-push-proxy](https://hub.docker.com/r/mattermost/mattermost-push-proxy) - Mattermost Push Proxy. Documentation: https://developers.mattermost.com/contribute/mobile/push-notifications/service/ GitHub: https://github.com/mattermost/mattermost-push-proxy

- [mattermost/mattermost-operator](https://hub.docker.com/r/mattermost/mattermost-operator) - Official image for Mattermost Operator for Kubernetes. For more information: https://github.com/mattermost/mattermost-operator

- [mattermost/mattermost-test-enterprise](https://hub.docker.com/r/mattermost/mattermost-test-enterprise) - Repository where all testing images is publish for any type of testing. Those images are build from the CircleCI Pipelines from the [mattermost-server](https://github.com/mattermost/mattermost-server) and [mattermost-webapp](https://github.com/mattermost/mattermost-webapp)

- [mattermost/mattermost-test-team](https://hub.docker.com/r/mattermost/mattermost-test-team) - Repository where all testing images is publish for any type of testing. Those images are build from the CircleCI Pipelines from the [mattermost-server](https://github.com/mattermost/mattermost-server) and [mattermost-webapp](https://github.com/mattermost/mattermost-webapp)

- [mattermost/mattermost-prod-app](https://hub.docker.com/r/mattermost/mattermost-prod-app) - Community driven image for Mattermost Server. **This Docker repository will be deprecated in Mattermost 6.0**. For more information and to check the dockerfile please refer to https://github.com/mattermost/mattermost-docker

- [mattermost/mattermost-prod-db](https://hub.docker.com/r/mattermost/mattermost-prod-db) - Community driven image for Database to run together with **mattermost/mattermost-prod-app**. **This Docker repository will be deprecated in Mattermost 6.0**. For more information and to check the dockerfile please refer to https://github.com/mattermost/mattermost-docker

- [mattermost/mattermost-prod-web](https://hub.docker.com/r/mattermost/mattermost-prod-web) - Community driven image for WebServer to run together with **mattermost/mattermost-prod-app**. **This Docker repository will be deprecated in Mattermost 6.0**. For more information and to check the dockerfile please refer to https://github.com/mattermost/mattermost-docker

- [mattermost/mattermost-preview](https://hub.docker.com/r/mattermost/mattermost-preview) - This is a Docker image to install Mattermost in Preview Mode for exploring product functionality on a single machine using Docker. Preview image Docs: http://bit.ly/1W76riY. GitHub: https://github.com/mattermost/mattermost-docker-preview

- [mattermost/platform](https://hub.docker.com/r/mattermost/platform) - Mirror of **mattermost/mattermost-preview**. This is a Docker image to install Mattermost in Preview Mode for exploring product functionality on a single machine using Docker. Preview image (mirror). Docs: http://bit.ly/1W76riY. GitHub: https://github.com/mattermost/mattermost-docker-preview

- [mattermost/mattermost-loadtest](https://hub.docker.com/r/mattermost/mattermost-loadtest) - Image for the Load Test application. Tools for profiling Mattermost under heavy load. GitHub: https://github.com/mattermost/mattermost-load-test

- [mattermost/sync-helpwanted-tickets](https://hub.docker.com/r/mattermost/sync-helpwanted-tickets) - For Internal usage. This iamge runs the sync with Jira tickets and GitHub Issues. To check the code please refer to https://github.com/mattermost/mattermost-utilities/tree/master/github_jira_tools

- [mattermost/mattermost-build-server](https://hub.docker.com/r/mattermost/mattermost-build-server) - Image used to build Mattermost used in CI. To check the Docker file refer to https://github.com/mattermost/mattermost-server/blob/master/build/Dockerfile.buildenv

- [mattermost/mattermost-build-webapp](https://hub.docker.com/r/mattermost/mattermost-build-webapp) - Image used to build Mattermost Webapp used in CI. To check the Docker file refer to https://github.com/mattermost/mattermost-webapp/blob/master/build/Dockerfile

- [mattermost/mattermost-marketplace-build](https://hub.docker.com/r/mattermost/mattermost-marketplace-build) - Image used to build Mattermost Marketplace. For more information please refer https://github.com/mattermost/mattermost-marketplace

- [mattermost/podman](https://hub.docker.com/repository/docker/mattermost/podman) - Internal usage. Contain Podman to build/tag/push container images

- [mattermost/mattermost-wait-for-dep](https://hub.docker.com/r/mattermost/mattermost-wait-for-dep) - Image used to wait for the other containers to start. Used in in CI and for local developement. Please refer to https://github.com/mattermost/mattermost-server/blob/master/docker-compose.yaml for more information.

- [mattermost/mattermost-elasticsearch-docker](https://hub.docker.com/r/mattermost/mattermost-elasticsearch-docker) - Used in in CI and for local developement. Please refer to https://github.com/mattermost/mattermost-server/blob/master/docker-compose.yaml for more information.

- [mattermost/webrtc](https://hub.docker.com/repository/docker/mattermost/webrtc) - DEPRECATED. Preview docker image of Mattermost WebRTC. Docs: http://bit.ly/2fVbWjU

- [mattermost/mattermost-cloud](https://hub.docker.com/r/mattermost/mattermost-cloud) - Mattermost Private Cloud is a SaaS offering meant to smooth and accelerate the customer journey from trial to full adoption. For more information see https://github.com/mattermost/mattermost-cloud