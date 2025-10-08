

## Content

this repo will be created and managed by system repository https://github.com/padreSVK/experimental_.checkout-system

all backstage entities will be in namespace `experiments`, for all referenes use full qualified name <kind>:<namespace>/<name>
all entities have owner group:experiments/team-alpha and belongs under system `checkout`


* Create kind: API, type: openapi (checkout-v1-api, checkout-v2-api)
  * v1 (in definition `$text: http://dotnet-demo.flux-test-tenant.svc.cluster.local/.less-known/api-docs/v1.json`)
  * v2 (in definition `$text: http://dotnet-demo.flux-test-tenant.svc.cluster.local/.less-known/api-docs/v2.json`)

* create Kind Component, type: react-application (checkout-web-app)
  * Uses API v1 and v2 

* Create Kind Resource type: postgresql (postgresql-checkout)
* Create Kind Resource type: kafka-topic (kafka-topic-orders)
* Create Kind Resource type: pqsql-database-access (dotnet-api-checkout) 3x for production development and staging
  * in spec:
    ```
    provideAccess: component:experiments/dotnet-api-checkout
    dependencyOf:
        - component:experiments/dotnet-api-checkout
    environment: "development"
    ```
* Create Kind Component type: dotnet-api (dotnet-api-checkout)
  * depends on
    * postgresql-checkout
    * kafka-topic-orders
    * dotnet-api-checkout
    * resource:experiments/checkout-main-mssql-database (do not create only reference)
  * provide API
    * checkout-v1-api
    * checkout-v2-api



