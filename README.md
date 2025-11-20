# Implementing a Multi-Environment Application Deployment with Kustomize

## Project Overview

This capstone project demonstrates deploying a web application in a Kubernetes environment using **Kustomize** to manage multiple environment configurations efficiently. The application will have distinct configurations for **development**, **staging**, and **production** environments, all integrated into a **CI/CD pipeline** for automated deployment.

**Key Objectives:**
- Learn to structure Kubernetes resources using Kustomize `base` and `overlays`.
- Customize configurations per environment (replicas, resource limits, environment variables).
- Securely manage secrets and ConfigMaps.
- Integrate Kustomize deployments with a CI/CD pipeline (GitHub Actions or Jenkins).
- Use advanced Kustomize features like Transformers and Generators.

---

## **Project Structure**

```
kustomize-capstone/
├── base/
│   ├── deployment.yaml
│   ├── service.yaml
│   └── kustomization.yaml
├── overlays/
│   ├── dev/
│   │   └── kustomization.yaml
│   ├── staging/
│   │   └── kustomization.yaml
│   └── prod/
│       └── kustomization.yaml
├── .gitignore
└── README.md
```

- **base/**: Contains common Kubernetes resources shared across environments.
- **overlays/**: Contains environment-specific customizations that patch the base resources.
- **.gitignore**: Excludes unnecessary files such as local configs or secrets.

---

## **Implementation Steps**

### 1. Project Setup
- Create a project directory:
```bash
mkdir kustomize-capstone && cd kustomize-capstone
```
- Create `base` and `overlays` directories:
```bash
mkdir -p base overlays/dev overlays/staging overlays/prod
```

### 2. Initialize Git
```bash
git init
touch .gitignore
```
- Add entries to `.gitignore` to exclude local files, secrets, and build artifacts.

### 3. Define Base Configuration
- Inside `base/`, create Kubernetes resources (Deployment, Service, etc.).
- Example `base/kustomization.yaml`:
```yaml
resources:
  - deployment.yaml
  - service.yaml
```

### 4. Create Environment-Specific Overlays
- Each overlay folder contains a `kustomization.yaml` that patches base resources:
```yaml
bases:
  - ../../base
patchesStrategicMerge:
  - deployment-patch.yaml
```
- Customize replica counts, resource limits, and environment variables for each environment.

### 5. Manage ConfigMaps and Secrets
- Use `configMapGenerator` and `secretGenerator` in overlays to handle configuration data securely.
- Example:
```yaml
configMapGenerator:
  - name: app-config
    literals:
      - ENV=development
secretGenerator:
  - name: db-secret
    literals:
      - DB_PASSWORD=supersecret
```

### 6. Integrate with CI/CD Pipeline
- Choose a CI/CD platform (e.g., GitHub Actions, Jenkins).
- Configure pipeline to:
  1. Detect code changes.
  2. Apply Kustomize manifests to the Kubernetes cluster.
  3. Deploy updated application automatically.

### 7. Test the CI/CD Pipeline
- Make changes in overlays or base configuration.
- Push changes to the repository.
- Verify pipeline deploys changes correctly to the Kubernetes cluster.

### 8. Advanced Features (Optional)
- Use **Transformers** for common labels and annotations.
- Use **Generators** to handle dynamic configurations.

---

### STEPS TAKEN IN THE PROJECT

1. Project Dir

![proj dir](image.png)

2. Base yaml file


![base yaml dir](image-1.png)

3. Base deployment.yaml file 

![base deploment.yaml](image-2.png)

4. Base service.yaml file

![base yaml file](image-3.png)

5. Base kudtomization .yaml file

![kustomization.yaml](image-4.png)

6. Overlays dev yaml file

![dev yaml](image-5.png)

7. Deployment-patch dev

![deployment-patch](image-6.png)

8. Kustomization.yaml development env

![kustomization.yaml](image-7.png)

9. Staging yaml file Dir

![staging](image-8.png)

10. Deployment-patch staging env

![deployment patch](image-9.png)

11. Kustomization.yaml staging env

![kustomization.yaml](image-10.png)

12. Production yaml file Dir prod env

![prod dir](image-11.png)

13. Deployment-Patch.yaml file prod env

![patch.yaml prod](image-12.png)

14. Kustomization.yaml prod env

![kustomization.yaml](image-13.png)

15. kubectl kustomize overlays/dev development env

![Kubectl kustomize](image-14.png)

16. kubectl Error minikube was not started to get kubectl get all -n default, Kubectl get nodes and kubectl get svc so i did `minikube start --driver=docker to get minikube started.

![error](image-15.png)

17. minikube start and kubectl get nodes

![start minikube](image-16.png)

18. kubectl apply -k dev env

![apply -k](image-17.png)

19. Kubectl kustomize overlays/staging

![staging kustomize](image-18.png)


20. Kubectl apply -k staging env and staging namespace

![apply -k staging](image-19.png)

21. Kubectl get all

![kubectl get all](image-20.png)

22. Kubectl kustomize overlays/production env

![kustomize prod](image-21.png)

23. Kubectl apply -k prod env

![apply -k](image-22.png)

24. Minikube services

![services](image-23.png)

25. Welcome to nginx

![nginx](image-24.png)

26. .github/workflows/deploy.yml file


![deploy.yml](image-25.png)

27. Workflows dir

![workflows dir](image-26.png)

28. git init, add and commit

![git add](image-27.png)

29. Workflows deploy-dev.yaml dev env

![deploy-dev.yaml](image-28.png)

30. Workflows dir

![dir](image-29.png)

31. GitHub Secrets

![github secrets](image-30.png)

32. Eksctl create cluster --name advanced-kustomize-cluster --region eu-north-1

![cluater](image-31.png)

33. Deploy-dev.yaml file

![deploy-dev.yaml](image-32.png)

34. Deploy-staging.yaml 

![deploy-staging.yaml](image-33.png)

35. Nginx

![nginx ](image-34.png)

36. Eksctl cluster ready

![cluster](image-35.png)

37. Cluster created

![cluster created](image-36.png)

38. Ec2 instance created

![ec2](image-37.png)

39. security Groups created

![SG created](image-38.png)

40. Auto Scaling Group created

![ASG created](image-39.png)

41. Virtual Private Cloud created

![VPC created](image-40.png)

42. Subnets created

![subnets](image-41.png)

43. Route table created

![route table](image-42.png)

44. Kubectl get nodes and kubectl get ns

![kubectl get](image-43.png)

45. Kubectl get all -n default

![get all](image-44.png)

46. Service.yaml dev updated

![service.yaml](image-45.png)

47. Dev kustomization.yaml updated

![kustomization.yaml](image-46.png)

48. dev service-patch.yaml updated

![service-patch.yaml](image-47.png)

49. Kubectl get svc

![get svc](image-48.png)

50. WELCOME TO NGINX

![nginx](image-49.png)

51. .Github/Workflows

![deployed](image-50.png)

52. dev workflows deployed

![dev workflows](image-51.png)

53. Dev kustomization.yaml updated

![updated yaml file](image-52.png)

54. Production kustomization.yaml updated

![prod kustomization.yaml](image-53.png)

55. kustomization.yaml staging updated

![kustomization.yaml staging](image-54.png)

56. Updated yaml file Direcrories

![dir ](image-55.png)

57. kustomize build overlays/staging

![build staging](image-56.png)

58. kustomize build overlays/prod

![build prod](image-57.png)

59. kustomize build overlays/dev

![build dev](image-58.png)

60. Labels & Transformers dev

![L&T dev](image-59.png)

61. Labels & Transformers prod

![L&T prod](image-60.png)

62. Labels and Transformers staging

![L&T staging](image-61.png)

63. updated dir

![dir](image-62.png)

64. Kustomize build development env

![kustomize build dev](image-63.png)

65. kustomize build Production env

![kustomize build prod](image-64.png)

66. kustomize build staging env

![kustomize build staging](image-65.png)

67. clean up using eksctl delete cluster --name advenced-kustomize-cluster --region eu-north-1
to clean up created clusters

![clean up](image-66.png)


















## **Evaluation Criteria**
- Correct implementation of Kustomize features across environments.
- Successful integration and functionality of the CI/CD pipeline.
- Secure management of secrets and environment-specific configurations.
- Clarity, completeness, and professionalism of documentation.

---

## **Submission**
- Submit the Git repository link.
- Include a report describing your implementation strategy, challenges faced, and solutions.

---

## **References**
- [Kustomize Official Documentation](https://kustomize.io/)
- [Kubernetes Documentation](https://kubernetes.io/docs/home/)

