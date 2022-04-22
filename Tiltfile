allow_k8s_contexts(k8s_context())

load('ext://configmap', 'configmap_from_dict')
load('ext://secret', 'secret_yaml_generic')

k8s_yaml('./kube/namespace.yml')
k8s_yaml('./kube/ingress.yml')

k8s_yaml(configmap_from_dict('midstall-nextcloud-mariadb-config', namespace='midstall', inputs = {
  'MYSQL_HOST': '127.0.0.1',
  'MYSQL_ROOT_HOST': '%'
}))

k8s_yaml(configmap_from_dict('midstall-nextcloud-config', namespace='midstall', inputs = {
  'MYSQL_HOST': '127.0.0.1',
  'REDIS_HOST': '127.0.0.1',
  'NEXTCLOUD_TRUSTED_DOMAINS': 'cloud.midstall.com'
}))

k8s_yaml(secret_yaml_generic('midstall-nextcloud-mariadb-secret', namespace='midstall', from_env_file='./config/cloud.env'))
k8s_yaml(secret_yaml_generic('midstall-nextcloud-redis-secret', namespace='midstall', from_env_file='./config/cloud.env'))
k8s_yaml(secret_yaml_generic('midstall-nextcloud-secret', namespace='midstall', from_env_file='./config/cloud.env'))

k8s_yaml(secret_yaml_generic('midstall-mail-secret', namespace='midstall', from_env_file='./config/mail.env'))

include('./packages/mail/Tiltfile')
include('./packages/nextcloud/Tiltfile')
include('./packages/website/Tiltfile')