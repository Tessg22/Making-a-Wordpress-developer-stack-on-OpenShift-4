# Making a Wordpress developer stack on OpenShift 4

This project template provides a starter kit for managing your Wordpress site on Openshift with tools such as Nginx, Php-fpm, Phpmyadmin, Mariadb, Red Hat CodeReady and Tekton.

*Note: If your OpenShift cluster is publicly accessible, instead of Docker based build config you can make use of Source based build config:*

```
$ oc import-image tgabriel/openshift-nginx-phpfpm-s2i:1.0 --confirm
$ oc edit bc/wordpress
...
  strategy:
      sourceStrategy:
        from:
          kind: ImageStreamTag
          name: tgabriel/openshift-nginx-phpfpm-s2i:1.0
          namespace: openshift
        incremental: true
      type: Source
...
```

## What does the template do?

* Example Wordpress source code will be placed in the `/app/web` directory.
* Creates 2 containers (nginx and php-fpm) per each pod. Deploys Phpmyadmin and Mariadb.
* Creates Routes for Wordpress and Phpmyadmin applications.
* Creates Tekton resources (Pipeline, 2x Tasks, 2x PipelineResources, PipelineRun, TriggerTemplate, TriggerBinding, Trigger and EventListener).
