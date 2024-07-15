To schedule OpenShift Container 4 etcd backups with a cronjob.

Create a project.
$ oc new-project ocp-etcd-backup --description "Openshift Backup Automation Tool" --display-name "Backup ETCD Automation"

Create Service Account
$ oc apply -f sa-etcd-bkp.yml

Create ClusterRole
$ oc apply -f cluster-role-etcd-bkp.yml

Create ClusterRoleBinding
$ oc apply -f cluster-role-binding-etcd-bkp.yml

Add service account to SCC "privileged"
$ oc adm policy add-scc-to-user privileged -z openshift-backup

Create Backup CronJob
$ oc apply -f cronjob-etcd-bkp.yml

After creating CronJob, you can force the execution for validation with the command:
$ oc create job backup --from=cronjob/openshift-backup
