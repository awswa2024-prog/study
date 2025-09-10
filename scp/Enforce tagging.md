Implement AWS resource tagging strategy using AWS Tag Policies and Service Control Policies (SCPs)

https://aws.amazon.com/pt/blogs/mt/implement-aws-resource-tagging-strategy-using-aws-tag-policies-and-service-control-policies-scps/

1. SCPs can only be applied to member accounts in an organization. They have NO effect on users or roles in the management account.
2. ![alt text](images/fig1arun.png "Title")
https://d2908q01vomqb2.cloudfront.net/972a67c48192728a34979d9a35164c1295401b71/2021/10/26/fig1arun.png

step 1: create tag policy, AWS Organizations -> Policies -> Tag policies -> Create new tg policy. EC2CreationEnforceTag, in the property Targets, attach the relevant OU or accounts that we want to enforce the policy.
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

check the policy compliance at AWS Resource Groups -> Tagging -> Tag Policies

step 2: create a service control policies(SCP), AWS Organizations -> Policies -> Tag policies -> Create new tg policy, EC2TagEnforcement,  attach the relevant OU or accounts that we want to enforce the policy.
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyEC2CreationSCP1",
      "Effect": "Deny",
      "Action": [
        "ec2:RunInstances"
      ],
      "Resource": [
        "arn:aws:ec2:*:*:instance/*",
        "arn:aws:ec2:*:*:volume/*"
      ],
      "Condition": {
        "Null": {
          "aws:RequestTag/costcenter": "true"
        }
      }
    },
    {
      "Sid": "DenyEC2CreationSCP2",
      "Effect": "Deny",
      "Action": [
        "ec2:RunInstances"
      ],
      "Resource": [
        "arn:aws:ec2:*:*:instance/*",
        "arn:aws:ec2:*:*:volume/*"
      ],
      "Condition": {
        "Null": {
          "aws:RequestTag/team": "true"
        }
      }
    }
  ]
}
```

step 2.1 create one more policy for preventing deleting tags, DenyEC2DeleteTagsSCP1,  attach the relevant OU or accounts that we want to enforce the policy.
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyDeleteTag1",
      "Effect": "Deny",
      "Action": [
        "ec2:DeleteTags"
      ],
      "Resource": [
        "arn:aws:ec2:*:*:instance/*",
        "arn:aws:ec2:*:*:volume/*"
      ],
      "Condition": {
        "Null": {
          "aws:RequestTag/costcenter": "false"
        }
      }
    },
    {
      "Sid": "DenyDeleteTag2",
      "Effect": "Deny",
      "Action": [
        "ec2:DeleteTags"
      ],
      "Resource": [
        "arn:aws:ec2:*:*:instance/*",
        "arn:aws:ec2:*:*:volume/*"
      ],
      "Condition": {
        "Null": {
          "aws:RequestTag/team": "false"
        }
      }
    }
  ]
}
```

step 3. validation , 
| Tag Enforcement Test | Outcome | Expected Result |
|----------------------|---------|----------------|
| Without tags | Launch failed | Yes |
| With random tag key and value | Launch failed | Yes |
| With tag key costcenter and wrong tag value | Launch failed | Yes |
| With tag key team only and correct tag value | Launch failed | Yes |
| With both tag keys (costcenter & team) and correct tag value | Launch success | Yes |

if we tried to delete tag, this is expected
| Tag enforcement test | Outcome | Expected result |
|----------------------|---------|----------------|
| Add a new random tag key / value | Success | Yes |
| Remove the random tag key / value | Success | Yes |
| Remove the tag costcenter | Error | Yes |
| Remove the tag team | Error | Yes |
