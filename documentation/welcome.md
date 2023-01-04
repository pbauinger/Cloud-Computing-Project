# Startup local minikube node

make sure to start docker

then run

```console
minikube start
```

## code
create a python script with following content for testing:
```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello_world():
    return "<p>Hello, World!</p>"

if __name__ == "__main__":
    app.run(host='0.0.0.0')
```

create a docker file with following content for testing:
```docker
# syntax=docker/dockerfile:1

FROM python:3.8-slim-buster

# RUN mkdir /app
WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

COPY . .

CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0"]
```

change directory to the `/src` folder and run `docker build -t app .`

check if the image was built with `docker images`

afterwards run the image with `docker run -p 5001:5000 app:latest`

now you can see the output in a browser on `http://127.0.0.1:5001`

## now, do this with minikube <!-- TODO: heading name -->

`kubectl get nodes` shows you the nodes (e.g. minikube)

create a file called `deployment.yaml` and fill in
```yaml
apiVersion: v1
kind: Service
metadata:
  name: hello-python-service
spec:
  selector:
    app: hello-python
  ports:
  - protocol: "TCP"
    port: 6000
    targetPort: 5000
  type: LoadBalancer

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-python
spec:
  selector:
    matchLabels:
      app: hello-python
  replicas: 4
  template:
    metadata:
      labels:
        app: hello-python
    spec:
      containers:
      - name: hello-python
        image: app:latest
        imagePullPolicy: Always
        ports:
        - containerPort: 5000
```

then run `kubectl apply -f kubernetes/deployment.yaml` (in the `/src' directory)

check your pods with `kubectl get pods -owide`

all of them should be READY
