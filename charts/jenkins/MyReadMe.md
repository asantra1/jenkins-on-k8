# Some useful tips and tricks

1. The JcasC demo avaialble [here](https://github.com/jenkinsci/configuration-as-code-plugin/tree/master/demos)

2. If you are running the Kubernetes to Docker desktop MAC, then all the PVs mounting to hostpath will be inside docker desktop VM only. To access that VM, run the command below

```
docker run --rm -it --privileged --pid=host walkerlee/nsenter -t 1 -m -u -i -n sh

ls -l /var/lib/k8s-pvs/jenkins/pvc-9450e76e-737b-4714-9ae6-66fe26b00046/
```
> After checking the files, one can reestart the VM ( Docker Desktop) and check for the file persistence.

3. Pay attention to periodically copy the working directory to S3 for backup.
4. The Password of the jenkins can be obtained following the same
```
jsonpath="{.data.jenkins-admin-password}"
secret=$(kubectl get secret -n jenkins jenkins -o jsonpath=$jsonpath)
echo $(echo $secret | base64 --decode)
```
Running the above code , we found the password **q4WJkFfaMhI9skHBMt0vji**
