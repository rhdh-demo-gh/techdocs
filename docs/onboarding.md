# Onboarding Applications

To onboard an application to the internal developer portal you must add a _catalog-info.yaml_ file to your repository.

Use this template, being sure to replace everything between the `<>` braces.

```yaml
apiVersion: backstage.io/v1alpha1
kind: Component
metadata:
  name: <NAME>
  description: <DESCRIPTION>
  annotations:
    # Remove this if your application isn't using Argo CD
    argocd/app-selector: rhdh.app/name=parasol
    github.com/project-slug: rhdh-demo-gh/<REPO_NAME>
    backstage.io/techdocs-ref: "dir:."
  tags:
    - application
    - store
    - redhat
spec:
  type: service
  lifecycle: experimental
  owner: group:rhdh-demo-gh/<TEAM_NAME>
  system: parasol
  repository: https://github.com/rhdh-demo-gh/<REPO_NAME>
  dependsOn:
    # Add dependencies here. These are other items listed in the software catalog
    - resource:default/parasol-db
  providesApis:
    # If you provide or consumesApis list them here
    - default/parasol-store-app-api
---
apiVersion: backstage.io/v1alpha1
kind: API
metadata:
  name: <NAME>-api
  description: <DESCRIPTION>
  tags:
    - api
    - openapi
    - parasol
spec:
  type: openapi
  lifecycle: experimental
  owner: group:rhdh-demo-gh/<TEAM_NAME>
  definition: 
    $text: <LINK_TO_OPENAPI_SPEC>
```
