### Scope of the CKS
-------------------------

- Host OS Security :-
    - Remove unnecessary apps
    - UptoDate
    - Restrict IAM or SSH access

- K8S cluster Security :-
    - UptoDate components
        - ApiServer
        - Kubelet
        - ETCD
    - Restrict external Access
    - Authentication
    - Authorization
    - Administration Controller 
        - Node Restriction
        - Custom Policies (OPA)
    - Enable Audit Logging
    - CIS Benchmarking Tool
    - ETCD Security

- Application Security :-
    - No Hardcoded secrets in Docker or Repository
    - RBAC
    - Container Sandboxing
    - Container Hardening
        - Reduce Attach Surface
        - Run As User
        - RO file System (To make it Immutable)
    - Vulnerability Scan
    - mTLS / ServiceMesh

- https://www.youtube.com/watch?v=wqsUfvRyYpw

-------------------------
### Certificate Architecture
-------------------------

- CA (Certificate Authority)
- PKI (Public Key Infrastructure)
    - /etc/kubernetes/pki

        - apiserver-etcd-client.crt 
            - Used by API Server to communicate to etcd server
        - apiserver-etcd-client.key 
            - Used by API Server to communicate to etcd server
        - apiserver-kubelet-client.crt 
            - Used by API Server to communicate to kubelet
        - apiserver-kubelet-client.key 
            - Used by API Server to communicate to kubelet
        - apiserver.crt 
            - API Server Certificate
        - apiserver.key 
            - API Server Key
        - ca.crt 
            - Common CA Certificate
        - ca.key 
            - Common CA Key
        - front-proxy-ca.crt 
            - Kube-Proxy CA Certificate
        - front-proxy-ca.key 
            - Kube-Proxy CA Key
        - front-proxy-client.crt 
            - Used by API Server to communicate to kube-proxy
        - front-proxy-client.key 
            - Used by API Server to communicate to kube-proxy
        - sa.key
            - 
        - sa.pub

    - etcd/

        - ca.crt
            - ETCD CA certificate
        - ca.key
            - ETCD CA Key
        - healthcheck-client.crt
            - Health check client certificate
        - healthcheck-client.key
            - Health check client key
        - peer.crt
            - Used by etcd members to communicate with each other
        - peer.key
            - Used by etcd members to communicate with each other
        - server.crt
            - ETCD Server Certificate
        - server.key
            - ETCD Server key
        
    - Scheduler
        - Certificate used by Scheduler to connect Kube-API certificate, can be found inside
            - /etc/kubernetes/scheduler.conf file
                - Look for 
                    - "client-certificate-data" for certificate
                    - "client-certificate-key" for key

    - Controller-Manager
        - Certificate used by Controller-Manager to connect Kube-API certificate, can be found inside
            - /etc/kubernetes/controller-manager.conf file
                - Look for 
                    - "client-certificate-data" for certificate
                    - "client-certificate-key" for key

    - Kubelet
        - Certificate used by kubelet to connect Kube-API certificate, can be found inside
            - /etc/kubernetes/kubelet.conf file
                - Look for
                    - "client-certificate" for certificate
                    - "client-key" for key
        - Kubelet Server
            - /var/lib/kubelet/pki/
                - kubelet.crt
                    - kubelet server certificate
                - kubelet.key
                    - kubelet server key

- https://www.youtube.com/watch?v=gXz4cq3PKdg
- https://kubernetes.io/docs/concepts/overview/components
- https://kubernetes.io/docs/setup/best-practices/certificates

-------------------------
### Containers
-------------------------
- Container Isolation
    - Linux Namespaces  - Restrict what processes can see (Other process/user/filesystem)
    - CGroups           - Restrict the resource usage of a process (cpu/memory/disk)

- To create docker container with shared pid namespace
    - $ docker run --name c2 --pid=container:c1 -d ubuntu sh -c 'sleep 999d'
        - It will use container c1's namespace for processes

- https://www.youtube.com/watch?v=MHv6cWjvQjM

