allow_k8s_contexts(k8s_context())
secret_settings(True)

load('ext://configmap', 'configmap_from_dict')
load('ext://secret', 'secret_yaml_generic')

k8s_yaml('./kube/namespace.yml')
k8s_yaml('./kube/ingress.yml')

k8s_yaml(secret_yaml_generic('midstall-nextcloud-secret', namespace='midstall', from_env_file='./config/cloud.env'))
k8s_yaml(secret_yaml_generic('midstall-ldap-secret', namespace='midstall', from_env_file='./config/ldap.env'))

include('./packages/ldap/Tiltfile')
include('./packages/nextcloud/Tiltfile')
include('./packages/website/Tiltfile')