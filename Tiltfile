load('ext://configmap', 'configmap_from_dict')
load('ext://secret', 'secret_yaml_generic')

k8s_yaml('./kube/namespace.yml')
k8s_yaml('./kube/ingress.yml')

include('./packages/nextcloud/Tiltfile')
include('./packages/website/Tiltfile')

k8s_yaml(configmap_from_dict('midstall-nextcloud-mariadb-config', namespace='midstall', inputs = {
  'MYSQL_HOST': 'localhost',
  'MYSQL_ROOT_HOST': '%'
}))

k8s_yaml(configmap_from_dict('midstall-nextcloud-config', namespace='midstall', inputs = {
  'MYSQL_HOST': 'localhost',
  'REDIS_HOST': 'localhost'
}))

k8s_yaml(secret_yaml_generic('midstall-nextcloud-mariadb-secret', namespace='midstall', from_env_file='./config/cloud.env'))
k8s_yaml(secret_yaml_generic('midstall-nextcloud-redis-secret', namespace='midstall', from_env_file='./config/cloud.env'))
k8s_yaml(secret_yaml_generic('midstall-nextcloud-secret', namespace='midstall', from_env_file='./config/cloud.env'))