## RBAC

## Permissions
REG_CODE=us-east-1
CLUSTER_NAME=expense
ACC_ID=AWS Account ID

```
eksctl utils associate-iam-oidc-provider \
    --region $REG_CODE \
    --cluster $CLUSTER_NAME \
    --approve
```