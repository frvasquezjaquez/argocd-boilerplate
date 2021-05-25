# ArgoCD Repository Boilerplate

Repository template for GitOps using ArgoCD. With this repository, we want to be able to:
- Re-deploy our cluster state in case of an incident.
- Deploy our applications in multiple enviroments keeping in mind that each application could have different parameters depending of the environment.

## Requirements

* Helm 3
* [ArgoCD 2.0+](https://github.com/argoproj/argo-helm/tree/master/charts/argo-cd)


## Project Folders Structure
```
├── applications
│   ├── business-logic
│   │   └── nginx
│   │       ├── base
│   │       │   ├── deployment.yaml
│   │       │   ├── kustomization.yaml
│   │       │   └── service.yaml
│   │       └── overlays
│   │           ├── dev
│   │           │   ├── deployment.yaml
│   │           │   └── kustomization.yaml
│   │           ├── prod
│   │           │   └── kustomization.yaml
│   │           └── qa
│   │               └── kustomization.yaml
│   └── cluster-services
├── argo-core
│   ├── applications-definitions
│   │   └── nginx.yaml
│   ├── argo-init.yaml
│   └── projects
│       └── web-applications.yaml
└── README.md
```

**applications:** (Optional) In case that we use a `mono-repo` to store our cluster applications, we should use this folder.

* `busines-logic:` Folder to store applications which belongs to our busines. Ex: APIs, Front-Ends, etc. 
    - `nginx:` Sample application using the kustomize's structure.
* `cluster-services:` Folder to store applications which provide services to the full cluster and the applications running in it. Ex: Prometheus, Jaeger, etc.


**argo-core:** Folder where we store the ArgoCD main componentes. Ex: projects, applications, etc. 

* `applications-definitinions:` Folder where we should store the ArgoCD's [Application](https://argoproj.github.io/argo-cd/operator-manual/application.yaml) custom resources for each of our applications by each environments.

* `projects:` Folder where we should store the ArgoCD's [Project](https://argoproj.github.io/argo-cd/operator-manual/project.yaml) custom resources which we will use to group our applications.

* `argo-init.yaml:` File where we create the first Project and Applications to automate the process to deploy every YAML in the projects and application-definitions folders.