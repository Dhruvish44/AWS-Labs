# AWS Lab 17 – CloudFormation Stack: EC2 + ALB + ASG

## 📘 Overview
Use CloudFormation to automate the deployment of an EC2 Auto Scaling infrastructure behind an ALB.

---

## 🚀 Steps Performed
```text
1️⃣ Create Template File (stack.yaml)
```

```yaml
AWSTemplateFormatVersion: 2010-09-09
Description: "ALB + ASG Stack"
Parameters:
  InstanceType:
    Type: String
    Default: t2.micro
Resources:
  LaunchTemplate:
    Type: AWS::EC2::LaunchTemplate
    Properties:
      LaunchTemplateData:
        ImageId: ami-0abcdef1234567890
        InstanceType: !Ref InstanceType
        UserData:
          Fn::Base64: !Sub |
            #!/bin/bash
            yum install -y httpd
            systemctl start httpd
            systemctl enable httpd
  TargetGroup:
    Type: AWS::ElasticLoadBalancingV2::TargetGroup
    Properties:
      Port: 80
      Protocol: HTTP
      VpcId: vpc-xxxx
  ALB:
    Type: AWS::ElasticLoadBalancingV2::LoadBalancer
    Properties:
      Subnets:
        - subnet-xxxx
        - subnet-yyyy
      SecurityGroups:
        - sg-xxxx
  Listener:
    Type: AWS::ElasticLoadBalancingV2::Listener
    Properties:
      DefaultActions:
        - Type: forward
          TargetGroupArn: !Ref TargetGroup
      LoadBalancerArn: !Ref ALB
      Port: 80
      Protocol: HTTP
  AutoScalingGroup:
    Type: AWS::AutoScaling::AutoScalingGroup
    Properties:
      VPCZoneIdentifier:
        - subnet-xxxx
        - subnet-yyyy
      LaunchTemplate:
        LaunchTemplateId: !Ref LaunchTemplate
        Version: !GetAtt LaunchTemplate.LatestVersionNumber
      MinSize: 1
      MaxSize: 3
      DesiredCapacity: 2
      TargetGroupARNs:
        - !Ref TargetGroup
Outputs:
  ALBDNS:
    Description: "Application Load Balancer DNS"
    Value: !GetAtt ALB.DNSName
```

```text
2️⃣ Deploy Stack
aws cloudformation create-stack --stack-name dhruvish-alb-asg --template-body file://stack.yaml
✅ Stack launches full environment automatically.
```

---

## 🧠 Key Takeaways
- CloudFormation = Infrastructure as Code.  
- Stacks ensure reproducible deployments.  
- ALB + ASG = automated scalability and recovery.
