## Cert manager with lets encrypt

This repository is used to do a tutorial on how to use cert-manager with lets encrypt on GKE.

https://cert-manager.io/docs/tutorials/getting-started-with-cert-manager-on-google-kubernetes-engine-using-lets-encrypt-for-ingress-ssl/#6-install-cert-manager

**Cert-manager** is a Kubernetes-native certificate management controller that simplifies the process of obtaining, managing, and renewing TLS certificates within a Kubernetes cluster. It integrates seamlessly with Ingress resources and plays a crucial role in automating the certificate provisioning process. Here's an enhanced explanation of how cert-manager works in this context:

**Ingress and Certificate Resources**: In cert-manager, the journey begins when an Ingress resource is applied to your Kubernetes cluster. The Ingress resource specifies the rules for routing incoming traffic to different services within your cluster. However, for secure HTTPS connections, you also need TLS certificates.

**Certificate Creation:** Cert-manager, being the certificate management controller, monitors the Ingress resources in your cluster. When it detects a new or updated Ingress resource that specifies TLS settings, cert-manager takes action. It automatically creates a Certificate resource associated with the Ingress.

**CertificateRequest Creation:** Now, the Certificate resource acts as a request for a TLS certificate. Cert-manager proceeds to create a CertificateRequest resource, which is a Kubernetes custom resource kind. This CertificateRequest represents the intention to obtain a TLS certificate from a Certificate Authority (CA).

**CSR Generation:** The CertificateRequest resource initiates the process of creating a Certificate Signing Request (CSR). A CSR is a cryptographic request that contains the public key and other information necessary for the CA to issue a certificate. Cert-manager generates the CSR on behalf of the CertificateRequest.

**CA Interaction:** Cert-manager interacts with the configured CA, which can be an internal CA, Let's Encrypt, or another trusted CA, depending on your cluster's configuration. It submits the CSR to the CA and awaits the issuance of the TLS certificate.

**Certificate Issuance:** The CA processes the CSR and, if all conditions are met (e.g., domain ownership verification for Let's Encrypt), issues the TLS certificate.

**Certificate Retrieval:** Once the CA issues the certificate, cert-manager retrieves it and stores it securely within your Kubernetes cluster.

**Certificate Lifecycle Management:** Cert-manager continues to monitor the certificate's lifecycle. It handles certificate renewals, ensuring that your TLS certificates are always up-to-date and valid. If the certificate is nearing expiration, cert-manager will automatically request a renewal from the CA.

In summary, cert-manager simplifies the management of TLS certificates for your Ingress resources by automating the process, from certificate creation to renewal. It uses Kubernetes-native resources like Certificate and CertificateRequest to orchestrate the certificate provisioning process, ensuring your applications are secure with minimal manual intervention.
