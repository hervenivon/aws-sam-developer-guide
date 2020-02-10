# OnSuccess<a name="sam-property-function-onsuccess"></a>

A destination for events that were processed successfully\.

## Syntax<a name="sam-property-function-onsuccess-syntax"></a>

To declare this entity in your AWS SAM template, use the following syntax:

### YAML<a name="sam-property-function-onsuccess-syntax.yaml"></a>

```
  [Destination](#sam-function-onsuccess-destination): String
  [Type](#sam-function-onsuccess-type): String
```

## Properties<a name="sam-property-function-onsuccess-properties"></a>

 `Destination`   <a name="sam-function-onsuccess-destination"></a>
The Amazon Resource Name \(ARN\) of the destination resource\.  
*Type*: String  
*Required*: Conditional  
*CloudFormation Compatibility*: This property is similar to the `[OnSuccess](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-lambda-eventinvokeconfig-destinationconfig-onsuccess.html#cfn-lambda-eventinvokeconfig-destinationconfig-onsuccess-destination)` property of an `AWS::Lambda::EventInvokeConfig`\. SAM will add any necessary permissions to the auto\-generated IAM Role associated with this function to access the resource referenced in this property\.  
*Additional Notes*: If the type is Lambda/EventBridge, Destination is required\.

 `Type`   <a name="sam-function-onsuccess-type"></a>
Type of the resource referenced in the destination\. Supported types are `SQS`, `SNS`, `Lambda`, and `EventBridge`\.  
*Type*: String  
*Required*: No  
*CloudFormation Compatibility*: This property is unique to AWS SAM and does not have an AWS CloudFormation equivalent\.  
*Additional Notes*: If the type is SQS/SNS and the `Destination` property is left blank, then the SQS/SNS resource is auto generated by SAM\. To reference the resource, use `<function-logical-id>.DestinationQueue` for SQS or `<function-logical-id>.DestinationTopic` for SNS\. If the type is Lambda/EventBridge, `Destination` is required\.

## Examples<a name="sam-property-function-onsuccess--examples"></a>

### EventInvoke Configuration Example<a name="sam-property-function-onsuccess--examples--eventinvoke-configuration-example"></a>

Example of how to use EventInvokeConfig\.

Since no Destination is given for the SQS OnSuccess configuration, SAM will create a SQS queue and add any necessary permissions\. Since a Destination is given for the Lambda OnFailure configuration, SAM will only add the necessary permissions to this Lambda function to call the destination Lambda function\.

#### YAML<a name="sam-property-function-onsuccess--examples--eventinvoke-configuration-example--yaml"></a>

```
EventInvokeConfig:
  DestinationConfig:
    OnFailure:
      Destination:
        Ref: DestinationLambda
      Type: Lambda
    OnSuccess:
      Type: SQS
```