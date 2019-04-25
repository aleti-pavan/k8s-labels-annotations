# Kubernetes Manifests using labels and annotations

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