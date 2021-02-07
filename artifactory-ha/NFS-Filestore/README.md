1. Create a new node pool as part of your GKE cluster (size 1, no need auto scaler). **OR** create a new GCP instance (not part of the cluster)
2. Connect into instance with ssh/GCloud command.
3. Run the following commands:

```bash
apt-get -y update
apt-get -y install nfs-kernel-server

mkdir -p /data
mkdir -p /backup
chmod 777 /data
chmod 777 /backup
chown 1030:1030 /data
chown 1030:1030 /backup

```

4. Edit the file: /etc/exports and add the following lines:

```bash
/data       *(rw,sync,no_root_squash,no_subtree_check)
/backup       *(rw,sync,no_root_squash,no_subtree_check)
```

5. Restart the nfs server service

```bash
sudo systemctl restart nfs-kernel-server

sudo systemctl status nfs-kernel-server
```

6. Install Artifactory:
```
export NFS_IP=<NFS-SERVER-INTERNAL-IP>

helm upgrade --install artifactory-nfs --namespace artifactory-nfs center/jfrog/artifactory-ha \
--set artifactory.persistence.nfs.ip=${NFS_IP} -f values-nfs.yaml
```

