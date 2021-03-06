# AWS::Events::EventBusPolicy<a name="aws-resource-events-eventbuspolicy"></a>

The `AWS::Events::EventBusPolicy` resource creates an event bus policy for Amazon CloudWatch Events\. An event bus policy enables your account to receive events from other AWS accounts\. These events can trigger CloudWatch Events rules created in your account\. For more information, see [Sending and Receiving Events Between AWS Accounts](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/CloudWatchEvents-CrossAccountEventDelivery.html) in the *Amazon CloudWatch Events User Guide*\.

If you grant permissions using `Condition` and specifying an organization, then accounts in that organization must specify a `RoleArn` with proper permissions when they use `PutTarget` to add your account's event bus as a target\.

The permission policy on the default event bus can't exceed 10 KB in size\.

## Syntax<a name="aws-resource-events-eventbuspolicy-syntax"></a>

To declare this entity in your AWS CloudFormation template, use the following syntax:

### JSON<a name="aws-resource-events-eventbuspolicy-syntax.json"></a>

```
{
  "Type" : "AWS::Events::EventBusPolicy",
  "Properties" : {
      "[Action](#cfn-events-eventbuspolicy-action)" : String,
      "[Condition](#cfn-events-eventbuspolicy-condition)" : [Condition](aws-properties-events-eventbuspolicy-condition.md),
      "[Principal](#cfn-events-eventbuspolicy-principal)" : String,
      "[StatementId](#cfn-events-eventbuspolicy-statementid)" : String
    }
}
```

### YAML<a name="aws-resource-events-eventbuspolicy-syntax.yaml"></a>

```
Type: AWS::Events::EventBusPolicy
Properties : 
﻿  [Action](#cfn-events-eventbuspolicy-action) : String
﻿  [Condition](#cfn-events-eventbuspolicy-condition) : [Condition](aws-properties-events-eventbuspolicy-condition.md)
﻿  [Principal](#cfn-events-eventbuspolicy-principal) : String
﻿  [StatementId](#cfn-events-eventbuspolicy-statementid) : String
```

## Properties<a name="aws-resource-events-eventbuspolicy-properties"></a>

`Action`  <a name="cfn-events-eventbuspolicy-action"></a>
The action that you are enabling the other account to perform\. Currently, this must be `events:PutEvents`\.  
*Required*: Yes  
*Type*: String  
*Minimum*: `1`  
*Maximum*: `64`  
*Pattern*: `events:[a-zA-Z]+`  
*Update requires*: [No interruption](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-updating-stacks-update-behaviors.html#update-no-interrupt)

`Condition`  <a name="cfn-events-eventbuspolicy-condition"></a>
`Condition` is a JSON string that you can use to limit the event bus permissions that you're granting only to accounts that fulfill the condition\. Currently, the only supported condition is membership in a certain AWS organization\. For more information about AWS Organizations, see [What Is AWS Organizations?](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_introduction.html) in the *AWS Organizations User Guide*\.  
 `Condition` is a property of the [ AWS::Events::EventBusPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-events-eventbuspolicy.html) resource type\.  
If you specify `Condition` with an AWS organization ID and specify "\*" as the value for `Principal`, you grant permission to all the accounts in the named organization\.  
*Required*: No  
*Type*: [Condition](aws-properties-events-eventbuspolicy-condition.md)  
*Update requires*: [No interruption](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-updating-stacks-update-behaviors.html#update-no-interrupt)

`Principal`  <a name="cfn-events-eventbuspolicy-principal"></a>
The 12\-digit AWS account ID that you are permitting to put events to your default event bus\. Specify "\*" to permit any account to put events to your default event bus\.  
If you specify "\*" without specifying `Condition`, avoid creating rules that may match undesirable events\. To create more secure rules, make sure that the event pattern for each rule contains an `account` field with a specific account ID from which to receive events\. Rules with an account field do not match any events sent from other accounts\.  
*Required*: Yes  
*Type*: String  
*Minimum*: `1`  
*Maximum*: `12`  
*Pattern*: `(\d{12}|\*)`  
*Update requires*: [No interruption](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-updating-stacks-update-behaviors.html#update-no-interrupt)

`StatementId`  <a name="cfn-events-eventbuspolicy-statementid"></a>
An identifier string for the external account that you're granting permissions to\. If you later want to revoke the permission for this external account, you must specify this `StatementId`\.  
*Required*: Yes  
*Type*: String  
*Minimum*: `1`  
*Maximum*: `64`  
*Pattern*: `[a-zA-Z0-9-_]+`  
*Update requires*: [Replacement](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-updating-stacks-update-behaviors.html#update-replacement)

## Return Values<a name="aws-resource-events-eventbuspolicy-return-values"></a>

### Ref<a name="aws-resource-events-eventbuspolicy-return-values-ref"></a>

 When you pass the logical ID of this resource to the intrinsic `Ref` function, `Ref` returns the event bus policy ID, such as `EventBusPolicy-1aBCdeFGh2J3`\.

For more information about using the `Ref` function, see [Ref](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html)\.

## Examples<a name="aws-resource-events-eventbuspolicy--examples"></a>

### Grant Permission to One Account<a name="aws-resource-events-eventbuspolicy--examples--Grant_Permission_to_One_Account"></a>

The following example grants permission to one AWS account with an account ID of `111122223333`\. 

#### JSON<a name="aws-resource-events-eventbuspolicy--examples--Grant_Permission_to_One_Account--json"></a>

```
"SampleEventBusPolicy": {
    "Type": "AWS::Events::EventBusPolicy",
    "Properties": {
        "Action": "events:PutEvents",
        "Principal": "111122223333",
        "StatementId": "MyStatement"
    }
}
```

#### YAML<a name="aws-resource-events-eventbuspolicy--examples--Grant_Permission_to_One_Account--yaml"></a>

```
SampleEventBusPolicy: 
    Type: AWS::Events::EventBusPolicy
    Properties: 
        Action: "events:PutEvents"
        Principal: "111122223333"
        StatementId: "MyStatement"
```

### Grant Permission to an Organization<a name="aws-resource-events-eventbuspolicy--examples--Grant_Permission_to_an_Organization"></a>

The following example grants permission to all AWS accounts in the organization with an organization ID of `o-1234567890`\.

#### JSON<a name="aws-resource-events-eventbuspolicy--examples--Grant_Permission_to_an_Organization--json"></a>

```
"SampleEventBusPolicy": {
    "Type": "AWS::Events::EventBusPolicy",
    "Properties": {
        "Action": "events:PutEvents",
        "Principal": "*",
        "StatementId": "MyStatement",
        "Condition": {
            "Type": "StringEquals",
            "Key": "aws:PrincipalOrgID",
            "Value": "o-1234567890"
        }
    }
}
```

#### YAML<a name="aws-resource-events-eventbuspolicy--examples--Grant_Permission_to_an_Organization--yaml"></a>

```
SampleEventBusPolicy: 
    Type: AWS::Events::EventBusPolicy
    Properties: 
        Action: "events:PutEvents"
        Principal: "*"
        StatementId: "MyStatement"
        Condition: 
            Type: "StringEquals"
            Key: "aws:PrincipalOrgID"
            Value: "o-1234567890"
```