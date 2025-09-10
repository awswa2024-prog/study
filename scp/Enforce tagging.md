Implement AWS resource tagging strategy using AWS Tag Policies and Service Control Policies (SCPs)

https://aws.amazon.com/pt/blogs/mt/implement-aws-resource-tagging-strategy-using-aws-tag-policies-and-service-control-policies-scps/

1. SCPs can only be applied to member accounts in an organization. They have NO effect on users or roles in the management account.
2. ![alt text](images/fig1arun.png "Title")
https://d2908q01vomqb2.cloudfront.net/972a67c48192728a34979d9a35164c1295401b71/2021/10/26/fig1arun.png

step 1: create tag policy, AWS Organizations -> Policies -> Tag policies -> Create new tg policy
```json
{
  "tags": {
    "costcenter": {
      "tag_key": {
        "@@assign": "costcenter"
      },
      "tag_value": {
        "@@assign": [
          "CC102",
          "CC103",
          "CC104"
        ]
      },
      "enforced_for": {
        "@@assign": [
          "ec2:instance"
        ]
      }
    },
    "team": {
      "tag_key": {
        "@@assign": "team"
      },
      "tag_value": {
        "@@assign": [
          "Team1",
          "Team2",
          "Team3"
        ]
      },
      "enforced_for": {
        "@@assign": [
          "ec2:instance"
        ]
      }
    }
  }
}
```
