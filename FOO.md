```bash
oc apply -f - <<EOF
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: foo
  namespace: foo
spec:
  storageClassName: thin-csi
  accessModes:
  - ReadWriteMany
  resources:
    requests:
      storage: 1Gi
EOF

oc new-app quay.io/eformat/welcome:latest

oc set volume deployment/welcome --add --overwrite -t persistentVolumeClaim --claim-name=foo --name=tools-data --mount-path=/mnt
```
