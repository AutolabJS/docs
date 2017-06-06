TODO:

1. The TLS security settings have to be at least TLS v1.2 compliant, preferably TLS v1.3 compliant. Use the best cipher suites from OWASP recommendations.

**NOTE:**    
1. The passphrases of security certificates provide additional layer of security. But, passphrases require human to input password. We can't use them for automated SSH operations between `load balancer - gitlab` and `execution nodes - gitlab` situations.


A summary of security settings used in the application. Most of these settings are enforced in the following files.

* deploy/keys.sh
* deploy/keys.conf
* deploy/openssl.conf

The DNS naming hierarchy for issuing security certificates is as follows.

* application url: foo.com
* main server: ms.foo.com (only after making MS sit behind Kong gateway)    
    For now, main server uses certificate issued to foo.com
* gitlab: gitlab.foo.com (only after making gitlab sit behind Kong gateway)    
    For now, main server uses certificate issued to foo.com
* load balancer: lb.foo.com
* execution node-1: en1.foo.com
* execution node-2: en2.foo.com

The keys are at present stored for backup in the following directory structure.
```shell
deploy/keys/
       gitlab/ (contains SSH keys)
              load_balancer/
              execution_nodes/
                     execution_node_1/
                     execution_node_2/
                     execution_node_3/
                     execution_node_4/
                     execution_node_5/
       main_server/ (contains SSL keys)
       load_balancer/ (contains SSL keys)
       execution_nodes/ (contains SSL keys)
                     execution_node_1/
                     execution_node_2/
                     execution_node_3/
                     execution_node_4/
                     execution_node_5/
```

The keys used by the AutolabJS components are available in the following locations.
```shell
main_server/ssl
load_balancer/ssl
deploy/keys/gitlab/ssl
deploy/keys/gitlab/main_server
deploy/keys/gitlab/load_balancer
deploy/keys/gitlab/execution_nodes
```


Here are a few suggested BATS tests for `deploy/keys.sh`:
1) creation of freshly minted certificates at the right locations
2) all certificates having the configured information and nothing else
3) test for createCert() function using different inputs
4) test all certificates for compliance against different standards we talked about before. One test for each standard.

### References ###
1. [keylength](https://www.keylength.com/en/compare/) - a summary of security settings from experts
1. OWASP guidelines on [TLS](https://www.owasp.org/index.php/Transport_Layer_Protection_Cheat_Sheet), [Key Mgmt](https://www.owasp.org/index.php/Key_Management_Cheat_Sheet), [Authentication](https://www.owasp.org/index.php/Authentication_Cheat_Sheet)    
    1. The seems to be TLS-PSK (Pre-Shared Key) or TLS-SRP. We might be able to solve the mutual authentication problem with in the framework of TLS. Again see the OWASP page for details.
    1. Select one of the tools on the OWASP page and use it to test the weaknesses in our configuration / generated certificates. Such a tool can be used in the [BATS](https://github.com/sstephenson/bats) test script for keys.sh.
1. [Certificate pinning](https://www.owasp.org/index.php/Certificate_and_Public_Key_Pinning)    
    1. We can make `main server-load balancer` connection and `load balancer - execution node` connection that can go through TLSv1.2-SRP check with client certificate pinning. The main server to web browser connection would be through TLS v1.2 without SRP.
    1. On the down side, certificate pinning makes dynamic deployment of components really difficult. Think about the problems of any security setup for dynamic deployment / rotation / scale up.
1. Express.js [security best practices](https://expressjs.com/en/advanced/best-practice-security.html)
1. [SRP in SSL](https://matthewarcus.wordpress.com/2014/05/10/srp-in-openssl/)
1. OWASP [secure coding practices](https://www.owasp.org/index.php/OWASP_Secure_Coding_Practices_Checklist)
1. SSH key generation and usage guidelines - [Mozilla](https://wiki.mozilla.org/Security/Guidelines/OpenSSH), [GNOME](https://wiki.gnome.org/AccountsTeam/SSHKeyGuidelines), [ArchLinux](https://wiki.archlinux.org/index.php/SSH_keys), [ssh-keygen man page](https://www.ssh.com/ssh/keygen/), [gitlab](https://gitlab.com/gitlab-org/gitlab-ce/issues/3433)
1. Hardening SSH - [Mangus](https://ef.gy/hardening-ssh), [Kleppmann](https://martin.kleppmann.com/2013/05/24/improving-security-of-ssh-private-keys.html)
