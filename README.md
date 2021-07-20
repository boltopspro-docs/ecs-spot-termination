<!-- note marker start -->
**NOTE**: This repo contains only the documentation for the private BoltsOps Pro repo code.
Original file: https://github.com/boltopspro/ecs-spot-termination/blob/master/README.md
The docs are publish so they are available for interested customers.
For access to the source code, you must be a paying BoltOps Pro subscriber.
If are interested, you can contact us at contact@boltops.com or https://www.boltops.com

<!-- note marker end -->

# ecs-spot-termination configset

![CodeBuild](https://codebuild.us-west-2.amazonaws.com/badges?uuid=eyJlbmNyeXB0ZWREYXRhIjoiRklTdEFaMGNiYkcrYUdIV2lHVTVsWS9MTk03QXR5OHVjTEtHWWQ2dW84MThydjZITyt2MmRkMytYaFo4ekI3SENqUzNlaFZ4RXVIeVF5ZGt0bnJRak9BPSIsIml2UGFyYW1ldGVyU3BlYyI6Ik5kUTd2ZnE1Z0lING9IdSsiLCJtYXRlcmlhbFNldFNlcmlhbCI6MX0%3D&branch=master)

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

This configset installs a spot termination script that will continuously run and monitor for the spot two-minute warning.  Upon seeing the two-minute warning, it will drain the instance from the ECS Cluster.

## What are lono configsets?

Lono configsets allow CloudFormation [cfn-init](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-init.html) [configsets](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-init.html) that are typically embedded in the template to be reusable.  More info: [Lono Configsets docs](https://lono.cloud/docs/configsets/).

## Usage

Add to project Gemfile:

```ruby
git "ecs-spot-termination", git: "git@github.com:boltopspro/ecs-spot-termination"
```

Use `configset` to enable the configset for the blueprint.  Example:

configs/demo/configsets/base.rb:

```ruby
configset("ecs-spot-termination", resource: "SpotFleet")
```

This adds the configset to the `resource` with the logical id `SpotFleet` in your CloudFormation template.  The configset is added to the [Resources["SpotFleet"].Metadata.AWS::CloudFormation::Init](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-init.html) attribute of the `SpotFleet` resource.  You can confirm that it'll be used with the [lono configsets BLUEPRINT](https://lono.cloud/reference/lono-configsets/) command.

    lono configsets demo
