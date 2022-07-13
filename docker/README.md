# Dockerize Setup


To perform the same POC in dockerize environment, we can run the following commands-



        docker run --name data-prepper -p 4900:4900 -v /home/ec2-user/tracing/pipelines.yaml:/usr/share/data-prepper/pipelines.yaml -v ${pwd}/data-prepper-config.yaml:/usr/share/data-prepper/data-prepper-config.yaml  opensearchproject/data-prepper:latest


        docker-compose up


        