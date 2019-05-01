# Kubernetes Manifests using labels and annotations

Labels and Annotations can be used by all of the Kubernetes API Objects like Pod, Service, Deployment, Ingress, Secret, ReplicaSet, DemonSet, Jobs ... etc

Labels:
======

Below is an overview of the Kubernetes labeling syntax. There are 3 things you have to consider; label key (label prefix, label name) and label value.


Label Key
---------
        Label prefix
        ------------
            Label prefix is optional
            Label prefixes can be no longer than 253 characters
            Label prefix must be a DNS subdomain
            Label prefix can also be a series of DNS subdomains, separated by “.”
            Label prefixes have to end with “/”
        Label name
        ----------
            Label name is required
            Label names can be up to 63 characters
            Characters have to be alphanumeric characters
            Label names can also include “-”, “_” and “.”
            Label names have to begin and end with an alphanumeric character

Label value
-----------
        Label values can be up to 63 characters long
        Characters have to be alphanumeric characters
        Label values can also include “-”, “_” and “.”
        Label values have to begin and end with an alphanumeric character

Create pods with labels:
-----------------------

$ kubectl apply -f pod-label1.yml 

pod/label-test created

$ kubectl apply -f pod-label2.yml 

pod/label-test2 created


Check the Pod is running
------------------------

$ kubectl get po

NAME          READY     STATUS    RESTARTS   AGE

label-test    1/1       Running   0          8m
label-test2   1/1       Running   0          4s


With labels in the output
-------------------------

$ kubectl get po --show-labels

NAME          READY     STATUS    RESTARTS   AGE       LABELS

label-test    1/1       Running   0          9m        env=testing,owner=pavan,team=randd

label-test2   1/1       Running   0          56s       env=testing,owner=pavan,team=sales


Query pods based on labels
--------------------------

$ kubectl get po --selector team=randd

NAME         READY     STATUS    RESTARTS   AGE

label-test   1/1       Running   0          3m

$ kubectl get po --selector owner=pavan

NAME          READY     STATUS    RESTARTS   AGE

label-test    1/1       Running   0          9m

label-test2   1/1       Running   0          1m

We can replace --selector with -l for simplicity

$ kubectl get po -l owner=pavan

NAME          READY     STATUS    RESTARTS   AGE

label-test    1/1       Running   0          9m

label-test2   1/1       Running   0          1m

$ kubectl get po -l team=randd

NAME         READY     STATUS    RESTARTS   AGE

label-test   1/1       Running   0          9m


Now, Lets get the pods belong to the team sales and randd

$ kubectl get po -l 'team in (randd,sales)'

NAME          READY     STATUS    RESTARTS   AGE

label-test    1/1       Running   0          12m

label-test2   1/1       Running   0          4m

If you want remove both of these pods you can do by below command

$ kubectl delete pods -l 'team in (randd,sales)'

pod "label-test" deleted

pod "label-test2" deleted



Annotations:
===========

You can use Kubernetes annotations to attach arbitrary non-identifying metadata to objects. Clients such as tools and libraries can retrieve this metadata.

Annotations are NOT used to identify and select objects. The metadata in an annotation can be small or large, structured or unstructured, and can include characters not permitted by labels.

Like labels, annotations are also contains two parts 


Annotations are key/value pairs. 

Annotation key - (annotation prefix, annotation name)
Annotation Value - value

Annotation Key:
--------------

        Annotation Prefix:
        ------------------
            Annotation prefix is optional
            Annotation prefixes can be no longer than 253 characters
            Annotation prefix must be a DNS subdomain
            Annotation prefix can also be a series of DNS subdomains, separated by “.”
            Annotation prefixes have to end with “/”

        Annotation name
        ---------------
            Annotation name is required
            Annotation names can be up to 63 characters
            Characters have to be alphanumeric characters
            Annotation names can also include “-”, “_” and “.”
            Annotation names have to begin and end with an alphanumeric character

Annotation value
----------------
        Label values can be up to 63 characters long
        Characters have to be alphanumeric characters
        Label values can also include “-”, “_” and “.”
        Label values have to begin and end with an alphanumeric character

Lab for Annotations:
-------------------

$ kubectl apply -f pod-annotation1.yml 

pod/nginx-pod-annotation created