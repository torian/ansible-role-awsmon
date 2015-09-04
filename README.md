# Ansible role to install AWS Monitoring Scripts

This role will install [CloudWatch Monitoring Scripts](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/mon-scripts-perl.html)
and setup cronjobs in `/etc/cron.d`. Currently, the following metrics are reported:

  * Disk usage (percentage) for all mounted filesystems
  * Memory usage (percentage)

CloudWatch alarms will also be setup for:

  * Alarm on disk usage above 80% (as `Disk usage: <mount_point> (<instance_id>)`)

## Requirements

This role assumes that the instance has an `IAM role` that allows the creation
of cloudwatch metrics. An example could be:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Stmt1426849513000",
            "Effect": "Allow",
            "Action": [
                "cloudwatch:GetMetricStatistics",
                "cloudwatch:ListMetrics",
                "cloudwatch:PutMetricAlarm",
                "cloudwatch:PutMetricData",
                "cloudwatch:SetAlarmState"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```

## TODO

  * Alarm for memory
  * disk usage percentage as variable
  * Cloudwatch alarms toggle
  * Use aws credentials as an option

