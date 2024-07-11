inScope The Red Hat Developer Portal

Overview
inScope is the Red Hat Developer Portal. It is the single source you need to find everything related to Hybrid Cloud Console apps and services. inScope is built on top of Red Hat Developer Hub, also known as RHDH, which is Red Hat's productized and supported version of Backstage, the open source developer portal framework. inScope ingests information from app-interface and thus knows about all apps and services on-boarded with app-interface. That means that any app you are looking for is likely already there, with a ton of useful information about it like build and deploy pipelines, escalation policies, test results, deployments, and a lot more. Using inScope developers, quality engineers, SREs, and support folks can find anything they need to develop, deploy, and debug applications. Along side the apps themselves inScope provides a whole host of useful features such as hot news from around the platform, platform status and outage notifications, product documentation, and more. inScope aims to be the single place people in Red Hat need to go to see information about anything on the Hybrid Cloud Management platform, replacing the complex sets of bookmarks and mental models developers rely on today.

Enabling Features for your Apps
Without doing anything on your part any app on app-interface will show up in the inScope catalog. App-interface contains a wealth of information on our apps and services, so there's a lot there with out app teams needing to do anything. Escalation policies, SLIs, build and deploy pipelines, deployments and more are all there right now. However, other features require some minor configuration to light up. Integrations like Snyk, Jira, Ibutsu, Kafka and some more require labels be added to your app-interface app YAML. This is because we don't use consistent unique identifiers for our apps and services across all systems. Your app may be insights-foo in app-interface, FooConsole in Jira components, and hybrid-foo in Ibutsu. The inScope labels allow us to map your app to other services to light up more features. You can find information on how to configure these labels in the inScope User Guide here https://inscope.corp.redhat.com/docs/default/component/backstage-app/your_content/

Adding Your Documentation
A very powerful feature of inScope is the ability to display your documentation while keeping it co-located with your code (or anywhere you like) in simple markdown. There's no need to move your docs to another system, or create them in a CRM. You can store your docs right alongside your code in Github or Gitlab and then simply tell inScope that you'd like your docs ingested. All you need is your documentation stored in markdown in your repo in whatever directory structure you want. Just make sure the landing doc is called index.md. Next, add a file called mkdocs.aml to the root of your repo that points to your documentation. An example can be found here https://github.com/RedHatInsights/firelink-frontend/blob/master/mkdocs.yml and that's it! Next time inScope rebuilds the catalog it will index your docs. If your docs aren't stored in your repo but somewhere else there's just one more step, you need to add an annotation to app-interface to specify where they are. You can find full directions in the user guide here https://inscope.corp.redhat.com/docs/default/component/backstage-app/your_content/

User Settings
You can access your user settings from Settings in the lower left corner. In the Settings section you can see what groups you belong to, set your user preferences like light or dark mode, and more.

Featured News and News Stories
We built a custom news system for inScope that allows us to easily surface news and information right on the front page. Adding news items is very easy and doesn't require any code changes. It simply requires editing a JSON file. If are have a news item you'd like to add reach out to devprod on Slack and we'll point you to it. In the future this will be fully self serviceable but for now we want to help people through the process.

The Catalog and Entities
All of our apps end up in the Catalog. Entries in the catalog are called entities. We have two types of entities: Apps and Services. They exist in a hierarchical relationship. Apps map to apps in app-interface and contain higher level information relevant to all components of an app. An app entity will contain things like escalation policies, clusters and namespaces, github repos, build jobs, owners, and more. Service entities map to code components in app-interface and are more granular. The represent individual code projects and contain information that is more appropriate to that more granular level, like deployments on OpenShift clusters, issues in Jira, build pipelines, security vulnerabilities and more. If you are searching for something and unsure where to start the App is the best place, you can then use the app's Dependencies page to find and drill into its services.

App Entity Info
You will find the following information on App entity pages:
* Links to github repos for all services under the app
* Links to deploy pipelines for all services under the app
* Links to clusters and namespaces the app's services are deployed to 
* Links to the build jobs for the app's services
* The escalation policies
* SLOs 
* Ibutsu test results
Here is an example of an App Entity page showing a lot of information https://inscope.corp.redhat.com/catalog/default/component/compliance-app

Service Entity Info
You will find the following on Service Entity pages:
* Jira issues and the link to open new Jira issues
* Snyk vulnerability reports
* Kafka lag metrics and active consumer groups
* OpenShift deployments including health metrics
* CI pipelines including github actions, jenkins, and tekton
* Progressive delivery topology
* Web RCA Incidents
Here is an example of a Service Entity showing a lot of information https://inscope.corp.redhat.com/catalog/default/component/insights-host-inventory
Note that Entity Pages features often require configuration in app-interface to light up. See the user guide for more information

Getting Help
You can consult the inScope user guide here https://inscope.corp.redhat.com/docs/default/component/backstage-app/ for self service learning and help. However, if you need additional help or want to report a bug reach out to Dev Prod on Slack at @crc-team-devprod

OpenAPI
You can easily hook up your OpenAPI specs to inScope so people can discover, view, and interact with your APIs right on the portal. It is as simple as adding the label rhdh/as-openapi/${UNIQUE_ID}: URL to reach your open API spec JSON. Example: rhdh/as-openapi/insights-host-inventory: https://console.redhat.com/api/inventory/v1/openapi.json to your app.yml in app-interface. After making that change your OpenAPI spec will show up linked from your App entity page and in the API section on the left after the next catalog ingest.

