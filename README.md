# Velero

## Velero installation

- Create velero namespace:

```bash
oc create new-project velero
```

- Add velero label to your volumesnapshotclass:

```bash
oc edit volumesnapshotclass/csi-vsphere-vsc

labels:
  velero.io/csi-volumesnapshot-class: "true"
```
- Complete values-paas.yaml
- Install velero helm chart:

```bash
helm install velero -f values-paas.yaml .
```

## Velero client installation

Folow below instructions to install velero client:

```bash
https://github.com/vmware-tanzu/velero/releases/download/v1.10.2/velero-v1.10.2-linux-amd64.tar.gz
tar xzf velero-v1.10.2-linux-amd64.tar.gz
mv velero-v1.10.2-linux-amd64/velero /usr/local/bin/
```

## Backup creation using velero client

```bash
velero  backup create $BACKUP_NAME
```
Some options:
- --include-namespaces
- --exclude-namespaces
- --snapshot-volumes=true

Note: default value for -include-namespaces is *

## Restoring backup using velero client

```bash
velero restore create --from-backup $BACKUP_NAME
```

Some options:
- --restore-volumes=true

## Schedule backup using velero cleint

```bash
velero schedule create $SCHEDULE_BACKUP_NAME --schedule="0 0 * * *"
```

Some options:
- --include-namespaces
- --exclude-namespaces
- --snapshot-volumes=true

Note: default value for -include-namespaces is *

## Some useful velero client commands

```bash
velero backup get
velero backup describe $BACKUP_NAME
velero backup logs $BACKUP_NAME

velero restore get
velero restore describe $RESTORE_NAME

velero schedule get
```