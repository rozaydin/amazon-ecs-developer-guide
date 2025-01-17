# Control access to Amazon ECS resources using resource tags<a name="control-access-with-tags"></a>

When you create an IAM policy that grants users permission to use Amazon ECS resources, you can include tag information in the `Condition` element of the policy to control access based on tags\. This is known as attribute\-based access control \(ABAC\)\. ABAC provides better control over which resources a user can modify, use, or delete\. For more information, see [What is ABAC for AWS?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_attribute-based-access-control.html)

For example, you can create a policy that allows users to delete a cluster, but denies the action if the cluster has the tag `environment=production`\. To do this, you use the `aws:ResourceTag` condition key to allow or deny access to the resource based on the tags that are attached to the resource\.

```
"StringEquals": { "aws:ResourceTag/environment": "production" }
```

To learn whether an Amazon ECS API action supports controlling access using the `aws:ResourceTag` condition key, see [Actions, resources, and condition keys for Amazon ECS](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazonecs.html)\. Note that the `Describe` actions do not support resource\-level permissions, so you must specify them in a separate statement without conditions\.

For example IAM policies, see [Example policies ](iam-policies-ecs-console.md)\. 

If you allow or deny users access to resources based on tags, you must consider explicitly denying users the ability to add those tags to or remove them from the same resources\. Otherwise, it's possible for a user to circumvent your restrictions and gain access to a resource by modifying its tags\.