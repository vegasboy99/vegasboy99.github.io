## Installing Service Mesh on OCP cluster

Install Operators (in order)
-  OpenShift Elasticsearch  <-- Will be storage for Jager data
-  Jager <-- Distributed Tracing
-  Kiali <-- Vizulization of the mesh
-  OpenShift Service Mesh

Deploy the control plane
- Create a seprate project to host the control plane workloads / In this case it'll be in the project ```istio-system```
- ```oc new-project istio-system```

- On the GUI confirm you're in that project and click on the operator for service mesh
- Under Istio Service Mesh Control Plane click Create ServiceMeshControlPlane.
- On the Create Service Mesh Control Plane page, modify the YAML for the default ServiceMeshControlPlane template as needed.

- Click the Istio Service Mesh Control Plane tab and drill down into the name of the CP

Creating the Red Hat OpenShift Service Mesh member roll
The ServiceMeshMemberRoll lists the projects that belong to the control plane. Only projects listed in the ServiceMeshMemberRoll are affected by the control plane. A project does not belong to a service mesh until you add it to the member roll for a particular control plane deployment.

You must create a ServiceMeshMemberRoll resource named default in the same project as the ServiceMeshControlPlane, for example istio-system.

To add your projects as members, modify the following example YAML. You can add any number of projects, but a project can only belong to one ServiceMeshMemberRoll resource. In this example, istio-system is the name of the control plane project.

```yml
apiVersion: maistra.io/v1
kind: ServiceMeshMemberRoll
metadata:
  name: default
  namespace: istio-system
spec:
  members:
    # a list of projects joined into the service mesh
    - ostoy
```

In the above example, I'm adding in the already existing ostoy project namespace

~
    
