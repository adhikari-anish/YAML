# YAML

- configuration files of Docker, Kubernetes, Ansible, Prometheus are all written in YAML
- widely used format
- for different DevOps tools and applications

## What is YAML?

YAML is a data serialization language just like XML, JSON.  

Serialization language: applications written with different languages, technologies, etc. which have different data structures can transfer data to each other using common standard format, and most popular such formats are YAML, XML, JSON.

YAML stands YAML Ain't Markup language.

File extension:  .yml or .yaml 

## YAML Format compared to others

- human readable and intuitive 

<image src='./images/Screen Shot 2022-09-05 at 9.19.13 PM.png' height="300px" />

Code is written in YAML using line separation and indentation.

## YAML Use Cases

* Docker Compose File
* Ansible
* Kubernetes

## Syntax of YAML

- key-value pairs

  ```yml
  app: user-authentication #string: can be wrapped in quotes or no quotes
  port: 9000 # number
  version: 1.7
  ```

- comments

  Comments are given using '#'

- objects

  objects are created like: 

    ```yml
    microservice:
      app: user-authentication
      port: 9000
      version: 1.7
    ```

  Here microservice is an object.

* lists

  Lists are created using dash (-).

  We can have multiple microservices like:
  
  ```yml
  microservices:
    - app: user-authentication
      port: 9000
      version: 1.7
    - app: shopping-cart
      port: 9002
      version: 1.9
  ```

  You can also have list inside list like: 
  ```yml
  microservices:
    - app: user-authentication
      port: 9000
      version: 1.7
    - app: shopping-cart
      port: 9002
      version:
      - 1.9
      - 2.0
      - 2.1
  ```

  If there are only primitive items we can put list inside [] like:

  ```yml
  microservices:
    - app: user-authentication
      port: 9000
      version: 1.7
    - app: shopping-cart
      port: 9002
      version: [1.9, 2.0, 2.1]
  ```

* booleans

  Booleans expressions are expressed using true, false, on, off, yes, no.

   ```yml
    microservices:
      - app: user-authentication
        port: 9000
        version: 1.7
        deployed: off
    ```
  
* multi-line strings

  ```yml
  multilineString: |
    this is a multiline string
    and this is the next line
    next line

  singlelineString: >
    this is a single line string, 
    that should be all on one line. 
    some other stuff
  ```

## Real Kubernetes Configuration Example

```yml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  containers:
  - name: nginx-container
    image: nginx
    ports:
    - containerPort: 80
    volumeMounts:
    - name: nginx-vol
      mountPath: /usr/nginx/html
  - name: sidecar-container
    image: some-image
```

Above we can find:
* key-value pairs
* metadata = object
* labels = object
* spec = object
* containers = list of objects
* ports = list
* volumeMounts = list of objects

## Environment variables

We can access environment variables using $ sign.

## Placeholders

Placeholders are written inside double curly braces like {{}} and this value gets replaced using template generator.

```yml
apiVersion: v1
kind: Service
metadata: 
  name: {{ .Values.service.name }}
spec: 
  selector:
    app: {{ .Values.service.app }}
  ports:
    - protoco: TCP
      port: {{ .Values.service.port }}
      targetPort: {{ .Values.service.targetport }}
```
