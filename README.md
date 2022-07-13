# Opensearch-Tracing


Tracing is an important factor while analysing our application. We often try to understand the issues occured in a microservice architecture, where the latency is high and which service did not response properly etc.

Tracing is one of the way to figure out your application issues and to see all the connections in the form of a service map.

The scope of this POC is understand how we can implement necessary components in kubernetes environment and send the traces to opensearch dashboard.

</br>

### POC Details 
-------------

- We will create a sample web based applicaiton with a few API endpoints with traces enabled at the code level.
- These traces will be pulled by Jaeger agent 
- Jaeger agent will fetch the traces and send to the collector.
- The open telemetry collector wil lsend the data to data-prepper.
- Data prepper will prepare the data to  be accepted by Opensearch.
- Finally, we will observe the data on Opensearch Tracing dashboard.

</br>

### Pre-Requisites
--------------------

- AWS Opensearch instance up and running in AWS.
- Kubernetes cluster where we will run the above mentioned components. 


### Setup
---------- 

1. Lets create the data prepper deployment in our kubernetes cluster. Make sure to update the data-prepper manifest file with opensearch URL and credentials.

            kubectl apply -f data-prepper.yaml 

2. Next, we will create jaeger-agent to pull the traces from our application. 

            kubectl apply -f jaeger-agent.yaml

3. Now, its time to create the otel collector by running the below command

            kubectl apply -f otel-collector.yaml

4. Finally, lets create our sample applicaiton

            kubectl apply -f sample-hotrod-app.yaml


- Now we have running pods, services and configmaps with all the required configurations.  
- The collection between these components are done by using the service endpoint.


</br>

### Access the application and traces
----------------------------------------

- The application will be accessible on a node port (defined in the sample-applicaiton service).
- Once the applicaiton is accessible, hit the buttons one by one to generate the traces.
- These traces will be processed and finally send to opensearch dashbaord. 
- We can access the opensearch dashboard --> Observability --> Trace Analytics

We should be seeing some tarces on the dashboard.


In case we do not see the traces within a few minutes, check the logs of each pod one by one to confirm if they are running fine.


