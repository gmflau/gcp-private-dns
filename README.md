# gcp-private-dns

```bash
export PROJECT_ID=$(gcloud info --format='value(config.project)')
export VPC_NETWORK="glau-vpc-network"
export DNS_ZONE=private-redis-zone
export DNS_SUFFIX=glau.redis.com
gcloud dns managed-zones create $DNS_ZONE \
    --description=$DNS_ZONE \
    --dns-name=$DNS_SUFFIX \
    --networks=$VPC_NETWORK \
    --labels=project=$PROJECT_ID \
    --visibility=private
```

```bash
gcloud dns record-sets create node1.${DNS_SUFFIX}. \
    --type=A --ttl=300 --rrdatas=10.122.0.89 --zone=$DNS_ZONE 
```
