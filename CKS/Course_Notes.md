#########################
##### Scope of the CKS
#########################

Host OS Security :-
    - Remove unnecessary apps
    - UptoDate
    - Restrict IAM or SSH access

K8S cluster Security :-
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

Application Security :-
    - No Hardcoded secrets in Docker or Repository
    - RBAC
    - Container Sandboxing
    - Container Hardening
        - Reduce Attach Surface
        - Run As User
        - RO file System (To make it Immutable)
    - Vulnerability Scan
    - mTLS / ServiceMesh

#########################
##### Architecture
#########################

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