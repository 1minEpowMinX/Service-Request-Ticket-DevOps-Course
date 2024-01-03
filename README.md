# Service-Request-Ticket-DevOps-Course  
**A practical exercise in troubleshooting**  

Subject: Service Request Ticket

Dear DevOps Engineer,

We have received a Service Request from our customer regarding an issue with api microservice version upgrading. After investigating the issue, we have identified that the problem is related to the deployment of the application using Helm.

We would like to ask for your assistance in reproducing the problem and troubleshooting the issue. 

Here are the steps to reproduce the problem:

1. Clone the application repository using the following command:

git clone --depth=1 https://github.com/den-vasyliev/go-demo-app.git

2. Install the application using Helm:
helm install current-version ./helm

3. This will deploy a bundle of microservices, databases, message broker and api-gateway with service called "ambassador".

4. Forward the service port to your local machine:

kubectl port-forward svc/ambassador 8080:80

5. Test the application by running the following command:

curl localhost:8080/api/

6. You should get the current version of the api microservice in the response: k8sdiy-api:599e1af

Finally, try to set new version and deploy a microservice using the following command:

helm template new-version ./helm -s templates/api-deploy.yaml --set image.tag=build-802e329

If you encounter an "ContainerCreating" message for Kubernetes pod, that is the first issue we need to resolve.

Second request. The new version of the api microservice should be deployed at the same endpoint as the current version but not available publicly. Only qa team should be able to access it.

We appreciate your prompt attention to this matter and we look forward to working with you to resolve this request. Please let us know if you have any questions or require further assistance.

Best regards!  

# Problem solving(May be supplemented in the future)  
The "ContainerCreating" issue was the need to update and implement app-configmap.yaml, secret.yaml, and update api-deploy.yaml and api-svc.yaml to implement testing of the Canary method via traffic scales and a special HTTP header for the QA team. All of these steps were necessary to migrate to the new version of the microservice.
