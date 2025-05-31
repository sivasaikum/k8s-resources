## Ingress Controller

## Permissions
REG_CODE=us-east-1
CLUSTER_NAME=expense
ACC_ID=344060441143
'''
eksctl utils associate-iam-oidc-provider \
    --region $REG_CODE \
    --cluster $CLUSTER_NAME \
    --approve

'''

'''
curl -o iam-policy.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.13.2/docs/install/iam_policy_us-gov.json

'''

'''
aws iam create-policy \
    --policy-name AWSLoadBalancerControllerIAMPolicy \
    --policy-document file://iam-policy.json

'''

'''
eksctl create iamserviceaccount \
--cluster=$CLUSTER_NAME \
--namespace=kube-system \
--name=aws-load-balancer-controller \
--attach-policy-arn=arn:aws:iam::$ACC_ID:policy/AWSLoadBalancerControllerIAMPolicy \
--override-existing-serviceaccounts \
--region $REG_CODE \
--approve

'''

## Install Drivers

'''
helm repo add eks https://aws.github.io/eks-charts
'''

'''
helm install aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system --set clusterName=$CLUSTER_NAME --set serviceAccount.create=false --set serviceAccount.name=aws-load-balancer-controller
'''
