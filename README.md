# nodejs-s2i

 
## Step 1 - Create a new namespace  
``` 
$ oc new-project nodejs-s2i-ex   
```


## Step 2 - Create a new project 
``` 
$ oc new-app image-registry.openshift-image-registry.svc:5000/openshift/nodejs~https://github.com/sclorg/nodejs-ex

example output:

--> Found container image 7e83665 (3 months old) from image-registry.openshift-image-registry.svc:5000 for "image-registry.openshift-image-registry.svc:5000/openshift/nodejs"

    Node.js 14 
    ---------- 
    Node.js 14 available as container is a base platform for building and running various Node.js 14 applications and frameworks.
    Node.js is a platform built on Chrome's JavaScript runtime for easily building fast, scalable network applications.
    Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient, perfect for data-intensive
    real-time applications that run across distributed devices.

    Tags: builder, nodejs, nodejs14

    * An image stream tag will be created as "nodejs:latest" that will track the source image
    * A source build using source code from https://github.com/sclorg/nodejs-ex will be created
      * The resulting image will be pushed to image stream tag "nodejs-ex:latest"
      * Every time "nodejs:latest" changes a new build will be triggered

--> Creating resources ...
    imagestream.image.openshift.io "nodejs" created
    imagestream.image.openshift.io "nodejs-ex" created
    buildconfig.build.openshift.io "nodejs-ex" created
    deployment.apps "nodejs-ex" created
    service "nodejs-ex" created
--> Success
    Build scheduled, use 'oc logs -f buildconfig/nodejs-ex' to track its progress.
    Application is not exposed. You can expose services to the outside world by executing one or more of the commands below:
     'oc expose service/nodejs-ex' 
    Run 'oc status' to view your app.
```  


## step 3 - Check to see if your application is running
```
$ oc get pods
NAME                         READY   STATUS      RESTARTS   AGE
nodejs-ex-1-build            0/1     Completed   0          13m
nodejs-ex-6d5b6c9b5d-rpjj5   1/1     Running     0          12m
```

## step 4 - Get the service and then expose it
```
$ oc get svc

NAME        TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
nodejs-ex   ClusterIP   xxx.xx.xx.xx   <none>        8080/TCP   38s


$ oc expose svc/nodejs-ex

route.route.openshift.io/nodejs-ex exposed
```

## step 5 - Check to see if your application is running
```

$ oc get route
NAME        HOST/PORT                                              PATH   SERVICES    PORT       TERMINATION   WILDCARD
nodejs-ex   nodejs-ex-nodejs-s2i-ex.xxxxxxxxxxxxxxxx         nodejs-ex   8080-tcp                 None
```


