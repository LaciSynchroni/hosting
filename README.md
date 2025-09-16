# Hosting
# Common Dependencies
- git
- docker (or podman if you are experienced)

# Choosing Deployments
After that, pick a setup you prefer and follow its readme. The following deployments are available:
- nginx: Simple, no prometheus or grafana, LetsEncrypt for certificates. No sharding, no file server replication. Not suited for large-scale (1000+ users)
