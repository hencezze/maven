# Maven+Java+Jenkins
This Jenkins build need plugins for correct work:
1. Nexus Artifact Uploader
2. Nexus Platform
3. Build Timestamp
4. Build Name and Description Setter
#
In Nexus, repository should will be name nexus
IP-Adresses are static and was writed into docker-compose file
Port-forwarding need for open UI in web on host
And other settings will be up, when I will have display how it works
#
For correct work need to create two pipelines:
1. backend, where java.app will have pull into Jenkins with dynamic name and start checking with Maven, when checking finished, our built artifact will upload in Nexus repository
2. test, where starts only if boolean parameter, which stay in backend pipeline code, be 'True'. In next step test will have make random value and create if-else job, which will have be true if random value takes digit 7 and stop with SUCCESS, in other case first pipeline will have stop with bad
#
Jenkins will have two users with different permissions:
1. dev user can see only 'backend' pipeline
2. test user can see only 'test' pipeline

## Script for fast base build


