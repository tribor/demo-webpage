---
marp: true
theme: uncover

---

# demo webseite
![bg blur opacity:.5](https://source.unsplash.com/random/?computer)

---

hier folgt eine aufzählung:
* erstens
* zweitens

![bg left:33%](https://source.unsplash.com/random/?writer)

---

<p class="text-center text-white text-9xl">Ende</p>

![bg cover](https://source.unsplash.com/random/?ende)


---
# deployment.yml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: demoinit
  name: demoinit
spec:
  replicas: 1
  selector:
    matchLabels:
      app: demoinit
  template:
    metadata:
      labels:
        app: demoinit
    spec:
      containers:
        - image: nginx
          name: webserver
          volumeMounts:
            - mountPath: /usr/share/nginx/
              name: webstorage
      initContainers:
        - name: init-webserver
          image: bitnami/git
          command:
            - sh
            - -c
            - git clone https://github.com/tribor/demo-webpage.git  /var/www/html/ --depth=1 --separate-git-dir /var/www/git
          volumeMounts:
            - mountPath: /var/www/
              name: webstorage
      volumes:
        - name: webstorage
          emptyDir:
