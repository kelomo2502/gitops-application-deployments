# Gitops Application Deployments
### Module 2: Application Deployment and Management in ArgoCD
#### Introduction
In this module, you'll gain hands-on experience with ArgoCD, focusing on deploying and managing applications. You’ll learn how to define applications in ArgoCD, manage their lifecycle, and structure Git repositories for optimal use with ArgoCD. 

#### Lesson 2.1: Defining and Deploying Applications with ArgoCD
**Objective**: Learn how to define and deploy applications using ArgoCD in a Kubernetes environment.
Steps:
1. Define an Application in ArgoCD
- Create a YAML file (`app-definition.yaml`) defining your application.
- Code snippet
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: sample-app
  namespace: argocd
spec:
  project: default
  source:
    repoURL: 'https://github.com/your-repo/sample-app.git'
    path: k8s
    targetRevision: HEAD
  destination:
    server: 'https://kubernetes.default.svc'
    namespace: sample-namespace

```

- Explanation: This YAML file specifies the application's source repository, the path within the repo, and the target Kubernetes cluster and namespace.

2. Deploy the Application:
- Apply the YAML file using `kubectl`.
`kubectl apply -f app-definition.yaml -n argocd`
- Explanation: This command tells ArgoCD to deploy the specified application according to the configuration in `app-definition.yaml`.

Resources:
[ArgoCD Application Declarative Setup](https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/)

#### Lesson 2.2: Managing Application Lifecycle: Syncing, Rollbacks, and Health Status
**Objective**: Understand how to manage the application lifecycle in ArgoCD.
Steps:
1. Syncing Application:
- Use ArgoCD CLI or UI to synchronize the application.
`argocd app sync sample-app`
- Explanation: This synchronizes the application's state with the desired state in the Git repository.

2. Monitoring Health and Status
- Check the application's health and sync status in ArgoCD UI or using CLI.
Command:
`argocd app get sample-app`
- Explanation: This command provides information on the sync and health status of your application.
3. Performing Rollbacks
- Rollback to a previous deployment state using ArgoCD UI or CLI.
Command:
`argocd app rollback sample-app`
- Explanation: This rolls back the application to its previous stable state.

**Resources**
[ArgoCD Application Lifecycle Management](https://argo-cd.readthedocs.io/en/stable/user-guide/application_lifecycle/)

#### Lesson 2.3: Structuring Git Repositories for Optimal ArgoCD Use
**Objective**: Learn how to structure Git repositories effectively for use with ArgoCD.
Steps:
1. Repository Structure
- Organize your repository with a clear structure, separating manifests, configurations, and environments.
Example structure:
├── k8s/
│   ├── dev/
│   │   └── deployment.yaml
│   └── prod/
│       └── deployment.yaml
├── src/
└── README.md
2. Environment Separation:
- Use different directories or branches for different environments (e.g., dev, staging, prod).
- Explanation: This helps in managing different configurations and ensures clarity.
3. Version Control Best Practices:
- Commit changes with meaningful messages and use tags/releases for versioning.

**Resources**
[Best Practices for Structuring Repositories](https://argo-cd.readthedocs.io/en/stable/user-guide/best_practices/)